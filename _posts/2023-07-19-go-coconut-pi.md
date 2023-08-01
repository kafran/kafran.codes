---
title: "Go: Server-Sent Events from a Raspberry Pi"
excerpt: "Creating a Raspberry Pi monitoring app with Go."
date: 2023-07-19T17:00:00-03:00
image: "/assets/images/posts/2022-11-15-swift-optionset/coqueiro.jpeg"
tags: 
  - go
---

I recently acquired a Raspberry Pi – specifically, the Raspberry Pi 3 model B+. Even though it isn't the latest in the Raspberry Pi series, it's a powerful and versatile device that offers a world of possibilities for computing hobbyists like myself. Acquiring this device here in Brazil wasn't an easy task, particularly due to the ongoing silicon shortage that has led to inflated prices.

Eager to explore its capabilities and simultaneously learn something new, I set out to create a monitoring application using Go – a robust language renowned for its simplicity and efficiency in handling concurrent operations. 

## My Mini-Project: A Monitoring App in Golang

My goal was to develop a dashboard that showcases various metrics from the Raspberry Pi, including temperature, clock speed, core voltage, and memory usage. The dashboard system is designed to serve these metrics to any subscribed client. As part of enhancing the project's capabilities, I chose to experiment with the recently introduced [Server-Sent Events extension of HTMX](https://deploy-preview-1650--htmx.netlify.app/extensions/server-sent-events/). This cutting-edge technology enables the server to push updates to a webpage over HTTP, establishing it as an exceptional tool for creating real-time applications."

Let's walk through some critical parts of the code.

### The Publisher-Subscriber Pattern

At the heart of the application is the Publisher-Subscriber pattern, a messaging pattern used in asynchronous programming to broadcast data to parts of a program that have subscribed to it. The Publisher struct holds a map of Subscriber pointers. When a Publish method is called on a Publisher, it sends the Event to each Subscriber in the map.

Initially, I implemented it using a `[]slice` to hold the subscribers, but a map proved to be more efficient for unsubscribing later. Since an empty struct in Go consumes 0 bytes, it's an excellent choice for the map value.

```go
type Event struct {
	Type string
	Data string
}

type Subscriber struct {
	Events chan Event
}

type Publisher struct {
	Subscribers map[*Subscriber]struct{}
	Mu          sync.RWMutex
}

func (p *Publisher) Subscribe() *Subscriber {
	p.Mu.Lock()
	defer p.Mu.Unlock()
	sub := &Subscriber{
		Events: make(chan Event),
	}
	p.Subscribers[sub] = struct{}{}
	defer fmt.Println("Subscriber subscribed ", sub)
	return sub
}

func (p *Publisher) Unsubscribe(sub *Subscriber) {
	p.Mu.Lock()
	defer p.Mu.Unlock()
	if _, ok := p.Subscribers[sub]; !ok {
		panic("Subscriber not found.")
	}
	delete(p.Subscribers, sub)
	close(sub.Events)
	defer fmt.Println("Subscriber unsubscribed ", sub)
}

func (p *Publisher) Publish(event Event) {
	p.Mu.RLock()
	defer p.Mu.RUnlock()
	for subscriber := range p.Subscribers {
		select {
		case subscriber.Events <- event:
		default:
			fmt.Println("Skipping event ", event)
		}
	}
}

func (p *Publisher) Size() int {
	p.Mu.RLock()
	defer p.Mu.RUnlock()
	return len(p.Subscribers)
}
```

Also, note the use of sync.RWMutex that allows multiple readers to access a resource at the same time, but only one writer. This is crucial to synchronize access to the Subscribers map in a multi-threaded environment, where many Goroutines could be attempting to read from or write to the map concurrently.

### Raspberry Pi Metrics

The PiMetric struct holds the command to retrieve a metric from the Pi, and a function to format that output into a more human-friendly form.

```go
type PiMetric struct {
	Name         string
	Command      []string
	FormatOutput func(output string) (string, error)
}
```

The runPiMetric function executes the command for each metric every second and publishes the output.

```go
func runPiMetric(metric PiMetric) {
	for {
		output, err := exec.Command(metric.Command[0], metric.Command[1:]...).Output()
		if err != nil {
			p.Publish(Event{metric.Name, "-"})
			fmt.Println(Event{metric.Name, err.Error()})
			continue
		}
		formattedOutput, err := metric.FormatOutput(string(output))
		if err != nil {
			p.Publish(Event{metric.Name, "-"})
			fmt.Println(Event{metric.Name, err.Error()})
			continue
		}
		p.Publish(Event{metric.Name, formattedOutput})
		time.Sleep(time.Second)
	}
}
```

### HTTP Handler for Subscribers

The piHandler function is an HTTP handler that responds with a stream of server-sent events. This allows a client to subscribe to updates from the server. The client's connection is kept alive, and the server pushes updates to the client as they occur.

```go
func piHandler(w http.ResponseWriter, r *http.Request) {
	flusher, ok := w.(http.Flusher)
	if !ok {
		http.Error(w, "Streaming not supported!", http.StatusInternalServerError)
		return
	}

	w.Header().Set("Content-Type", "text/event-stream")
	w.Header().Set("Cache-Control", "no-cache")
	w.Header().Set("Connection", "keep-alive")

	sub := p.Subscribe()
	defer p.Unsubscribe(sub)

	for {
		select {
		case event := <-sub.Events:
			fmt.Fprintf(w, "event: %s\ndata: %s\n\n", event.Type, event.Data)
			flusher.Flush()
		case <-r.Context().Done():
			return
		}
	}
}
```

### The Main Function

The main function initializes the HTTP server and starts the monitoring Goroutines. It serves static files from the `/` route, and the `/status` route uses the `piHandler` function to serve updates to subscribers. The static files are embedded into the binary for easy of deployment on the Raspberry Pi.

```go
func main() {
	http.Handle("/", http.FileServer(http.FS(views.Files)))
	http.HandleFunc("/status", piHandler)
	go monitor()
	http.ListenAndServe(":8080", nil)
}
```

### Wrapping Up

I've come to appreciate how Go's simplicity, coupled with its efficiency and concurrency model, makes it an ideal language for the backend needs of independent developers like me. I'm always excited to use Go in my projects and explore more of its capabilities.

You can see this project in action at https://coconutpi.kafran.codes. Please don't hack me 🥲.

You can find the source code on GitHub: https://github.com/kafran/coconut-pi.

Thanks for joining me on my journey learning Golang. Happy coding!

## About the image

This is close to my home in the city of João Pessoa, in the Northeast of Brazil. I love this area. A courious fact, aparently [coconut trees are more dangerous than sharks](https://en.wikipedia.org/wiki/Death_by_coconut).
