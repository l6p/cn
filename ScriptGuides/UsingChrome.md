---
sort: 6
title: Using Chrome
---

# Using Chrome In Testing

Add a `*web.Client` type parameter to the test case function, 
then the test framework will automatically inject the Web client for the test case to use.

`web.Client` wraps [chromedp](https://github.com/chromedp/chromedp){:target="_blank"} to make it more convenient to use.

`web.Client` initializes Chrome in Headless mode, which starts with the following parameters:

| Parameter | Description |
| --------- | ----------- |
| --disable-gpu | Disables GPU hardware acceleration. If software renderer is not in place, then the GPU process won't launch. |
| --no-default-browser-check | Disables the default browser check. Useful for UI/browser tests where we want to avoid having the default browser info-bar displayed. |
| --no-first-run | Skip First Run tasks, whether or not it's actually the First Run. Overridden by kForceFirstRun. This does not drop the First Run sentinel and thus doesn't prevent first run from occuring the next time chrome is launched without this flag. |
| --no-sandbox | Disables the sandbox for all process types that are normally sandboxed. Meant to be used as a browser-level switch for testing purposes only. |
| --headless | Run in headless mode, i.e., without a UI or display server dependencies. |
| --hide-scrollbars | Hide scrollbars from screenshots. |
| --mute-audio | Mutes audio sent to the audio device so it is not audible during automated testing. |

Chrome's `window-size` and `user-agent` can be adjusted in the system, and the default window size is **1920 * 1080**.

## Code example

```go
package main

import (
	"github.com/l6p/utils/client/web"
	"log"
	"time"
)

func SimpleCase(client *web.Client, logger *log.Logger) error {
	var example string
	client.Go(`https://golang.org/pkg/time/`).
		WaitVisible(`body > footer`).
		Click(`#pkg-examples > div`).
		Value(`#example_After .play .input textarea`, &example).
		Do()

	logger.Printf("Go's time.After example:\n%s", example)
	time.Sleep(10 * time.Second)
	return nil
}

func Export() map[string]interface{} {
	return map[string]interface{}{
		"SimpleCase": SimpleCase,
	}
}
```

## Reference

* [An example of a test script that uses Chrome](https://github.com/l6p/helm/tree/master/examples/using-chrome){:target="_blank"}
* [An example of local debugging Chrome test script](https://github.com/l6p/helm/tree/master/examples/using-chrome-with-local-debug){:target="_blank"}
