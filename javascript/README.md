
# Javascript

### Remove watched videos from WatchLater playlist from YouTube

This is an script I found on Reddit. As Google doesn't care about that the "Remove Watched Videos" button does not work at all, this script does it for you. It's not immediate but it gets the job done:

```javascript
javascript:(function () {var interval = setInterval(function () {var el = document.getElementsByClassName('pl-video'); var i = 0; while (i < el.length && el[i].getElementsByClassName('watched-badge').length === 0) {i++; } if (i < el.length) {el[i].getElementsByClassName('pl-video-edit-remove')[0].click(); } else {clearInterval(interval); } }, 500); })();
```
