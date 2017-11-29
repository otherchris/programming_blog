## 2017-11-29

- Prologue

  - At Nodevember I got curious about what's going on with the network
  connection on my machine

  - I'm alwatys interested in tooling and process so I thought "why don't I log
  all network activity on my ethernet interface?"

  - Step 0: what's a network interface, using tcpdump, estimating the scale of
  the data

- Act 1

  - Step 1: Log the tcpdump, compress, store on remote server, repeat.
    - Rabbit hole: A super quick Elixir endpoint

  - Step 2: Use logstash to read the log files into elasticsearch

- Act 2

  - Step 3: Processing logs with logstash, logstash dev env

- Act 3

  - Step 4: Historical data, what metrics to save?

-  Epilogue

  - ???

