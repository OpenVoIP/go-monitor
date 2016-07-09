# Simple server monitoring in Go

`go-monitor` is simple server monitoring written in Go. I was on the lookout for a tool which allowed me 
to monitor a list of services and notify me through SMS or email. Everything I found seemed a bit too complex 
and so `go-monitor` was born.

## TL;DR
`go-monitor` monitors a list of services as specified by the user and then notifies one or more users through SMS 
of any services that are down.

We use [MessageBird](https://www.messagebird.com/) as an SMS delivery service. SMS can be exchanged for a 
number of other services through MessageBird.

Config is read through a yaml file.
Users can specify how often they are notified of a given service being down through the `defaultttl` value in the config.

By default, processes are checked every 60 seconds. This can be increased or decreased depending on the importance of services.

This program is intended for use on Unix systems.

## Installation
1. Clone repo.

2. Install dependencies:

 `go get github.com/patrickmn/go-cache`
 `go get gopkg.in/yaml.v2`

3. Update `go-monitor.yml.sample` to include the configuration options desired. 

4. Copy config to `/usr/local/etc/go-monitor.yml`.

5. `go install`

6. Optional: use `init` file as script for use as a service. `go-monitor` must be placed in `/usr/local/etc/` for this script. Script should be placed in `/etc/init.d/`.

## How it works
We use a Go to push this onto the server:

`ps aux | grep PROCESS_NAME`

We then read the number of lines returned. Super simple.

## Additions
Down the line it would be nice to have server monitoring in addition to process monitoring:

- CPU
- Disks (usage, read/write)
- Memory

This could further be extended into network monitoring. Someday.

## License
MIT
