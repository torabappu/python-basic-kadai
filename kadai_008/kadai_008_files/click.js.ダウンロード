var DOMReady = function (a, b, c) {
    b = document, c = 'addEventListener';
    b[c] ? b[c]('DOMContentLoaded', a) : window.attachEvent('onload', a)
}
var atownClickEventHasBeenCalled = false;

function atownClickEvent() {
    if (atownClickEventHasBeenCalled || !('localStorage' in window) || (window.localStorage == null)) return;
    var params = location.search.substring(1).split('&');
    for (var i = 0; params[i]; i++) {
        var kv = params[i].split('=');
        if (kv[0] == 'atm_id') {
            var id = kv[1];
        } else if (kv[0] == 'affid') {
            var affid = kv[1];
        } else if (kv[0] == 'atm_tid') {
            var tid = kv[1];
        }
    }
    if (id != null && affid != null) {
        localStorage.setItem('affi_adv_' + id, affid);
    }
    atownClickEventHasBeenCalled = true;

    // ここで cross.js の script 要素を動的に追加する
    if (id) {
        var script = document.createElement('script');
        script.src = '//ad.atown.jp/lib/cross.js?aid=' + id;
        script.async = 1;
        var scriptNodes = document.getElementsByTagName('script');
        if (null != scriptNodes && 0 < scriptNodes.length) {
            // script 要素が見つかったので、その手前に insert
            scriptNodes[0].parentNode.insertBefore(script, scriptNodes[0]);
        } else {
            // script 要素が無かったので、head の末尾に append
            document.head.appendChild(script);
        }
    }

    // ITP
    if (id && affid && tid) {
        try {
            var fqdn = atob(tid);
            var xhr = new XMLHttpRequest();
            xhr.open('GET', '//' + fqdn + '/v1/lp?aid=' + id + '&s=' + affid, true);
            xhr.withCredentials = true;
            xhr.send(null);
        } catch (e) {
            // ignore
        }
    }
}

DOMReady(function () {
    atownClickEvent();
});
if (document.readyState == "complete") {
    atownClickEvent();
} else {
    document.onreadystatechange = function () {
        if (document.readyState == "complete") {
            atownClickEvent();
        }
    }
}
