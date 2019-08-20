```
ADT.Tag.doEvent = function (t, am, c, ti, tp, cpn, xd) {
    ADT.Tag.t = typeof ADT.Tag.t === "undefined" ? 3 : ADT.Tag.t;
    ADT.Tag.c = typeof ADT.Tag.c === "undefined" ? "SEK" : ADT.Tag.c;
    t = typeof t === "undefined" ? ADT.Tag.t : t;
    am = typeof am === "undefined" ? ADT.Tag.am : am;
    c = typeof c === "undefined" ? ADT.Tag.c : c;
    ti = typeof ti === "undefined" ? ADT.Tag.ti : ti;
    tp = typeof tp === "undefined" ? ADT.Tag.tp : tp;
    cpn = typeof cpn === "undefined" ? ADT.Tag.cpn : cpn;
    xd = typeof xd === "undefined" ? ADT.Tag.xd : xd;
​
    var saleQuery = "t=" + t + "&tk=" + ADT.Tag.tk + "&am=" + am + "&c=" + c + "&ti=" + ti + "&tp=" + tp + "&trt=" + ADT.Tag.trt + "&cpn=" + cpn + "&ap=" + ADT.Tag.ap + "&xd=" + xd + "&tt=1";
    var salePath = "/t/t";
    // check for at_gd cookie
    var guid = ADT.Tag.getCookieValue("at_gd");
    if (guid != null) {
        saleQuery += "&at_gd=" + guid;
    }
    var cn = ADT.Tag.getCN();
    if (cn != null) {
        var cv = ADT.Tag.getCookieValue(cn)
        saleQuery += "&cn=" + cn + "&cv=" + cv;
    }
​
    // webKit workaround for inApp browsers. See: https://bugs.webkit.org/show_bug.cgi?id=193508
    var userAgent = window.navigator.userAgent.toLowerCase(), downgrade = /samsungbrowser|crios|edge|gsa|instagram|fban|fbios/.test( userAgent );
​
    if (!navigator.sendBeacon || downgrade) {
        var imgEl = document.createElement("img");
        imgEl.src = ADT.Tag.eventHost + salePath + "?" + saleQuery;
        imgEl.width = 1;
        imgEl.height = 1;
        imgEl.style.cssText = "display:none";
        document.body.appendChild(imgEl);
        console.log("Triggered event using image element.");
    } else {
        navigator.sendBeacon(ADT.Tag.eventHost + salePath + "?" + saleQuery);
        console.log("Triggered event using beacon.");
    }
    console.log(ADT.Tag.eventHost + salePath + saleQuery);
};
```

