# Repro golang.org/issue/34374

This repository contains the minimal repro case. In order to test:

```
$ git clone https://github.com/hyangah/issue34374
$ cd issue34374

# if using python 2.X
$ python -m SimpleHTTPServer 8000 

# if using python 3.X
$ python -m http.server 8000
```

This will start a webserver on port 8000. Open http://127.0.0.1:8000 from the chrome browser.

# Files

Go execution trace program (`go tool trace <trace>`) starts 
a server that serves an html with a javascript, trace viewer
json format data files, and the vulcanized trace viewer file. 
It follows the instruction originally in https://chromium.googlesource.com/catapult/+/refs/heads/master/tracing/docs/embedding-trace-viewer.md.


 - index.html: main html page that imports trace_viewer_full.html and defines the data load javascript.
   It also contains the `origin-token` for `http://127.0.0.1:8000` as a temporary workaround.

 - data.json: data to render.

 - trace_viewer_full.html: generated with catapult's `tracing/bin/vulcanize_trace_viewer`.
   In order to regenerate the file

```
$ git clone https://chromium.googlesource.com/catapult
$ cd catapult
$ tracing/bin/vulcanize_trace_viewer --config=full
```


