***

**Which implementation of diff-patch Alg?**

**Where are the documents & the shadows?**

**How and why can we adjust the sync-cycle? What are the dis-/advantages?**

- The sync-cycle can be adjusted in the `client/index.js` file, Line 203-221
```javascript
var timeout = null;  
function processSend(value) {  
    clearTimeout(timeout);  
  
    var delay = parseInt($timeoutDelay.value);  
  
    // set the sync-cycle  
    if (delay > 0) {  
        $timeoutIndicator.innerHTML = "Processing...";  
        // set a timeout for the delay  
        timeout = setTimeout(() => {  
            $timeoutIndicator.innerHTML = "Sent!";  
            // send the patch to the server  
            sendPatch(value);  
        }, delay);  
    } else {  
        sendPatch(value);  
    }  
}
```

- This code is representing the `processSend` method
- if the set delay is > 0, then there is a set timeout that will be executed for that amount
- if delay is 0, then the patch will be sent immediately

- Advantages:
	- You are able to adjust the sync-cycle freely on the client-side, gives you some flexibility
- Disadvantages:
	- You are able to perhaps to some goofy stuff with it
	- Doing this goofy stuff may impact the applications performance and the work of the Diff-sync algorithm in general


**Where/How is the edit-Stack implemented?**

**Is it possible to deploy a Peer-to-Peer Version of Mr. Wei's implementation?**

- "peer-to-peer" = a client can be a server
- Yes, it is possible due to the fact, that both the client and the server are using the same Library (diff-sync)
- This can be seen, if you look at the initialization of the diff sync objects in both files:

- client/index.js:
```javascript
var diffSync = new module.exports({  
    jsonpatch,  
    thisVersion: "n",  
    senderVersion: "m",  
    useBackup: true,  
    debug: true  
});
```

- server.js:
```javascript
var diffSync = new DiffSyncAlghorithm({  
    jsonpatch: jsonpatch,  
    thisVersion: "m",  
    senderVersion: "n",  
    useBackup: true,  
    debug: true  
});
```



**How is it possible to use the API in other JS-Projects?**

**Are the JSON-Docs interchangable with other kind of Docs?**

**How is Mr. Wei solving the conflicts?**

**What are possible enhancements of Mr. Wei's Code? Should you suggest a pull-request?**

**Is it possible to combine diff-sync-js with a doc-oriented NoSQL-Datastore?**

