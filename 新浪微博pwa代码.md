
window.addEventListener("load", (function() {
  if ("serviceWorker"in window.navigator && !/; wv(;|\)).+ Chrome\/.+ Mobile/g.test(window.navigator.userAgent)) {
      var e, t = function t() {
          e && (e.prompt(),
          e.userChoice.then((function(e) {
              "accepted" === e.outcome ? (a["a"].removeData("prompt_dismissed"),
              console.log("User accepted the A2HS prompt")) : (a["a"].setData("prompt_dismissed", Date.now()),
              console.log("User dismissed the A2HS prompt"))
          }
          )),
          e = null,
          document.removeEventListener("click", t))
      }, n = window.config.version.replace("v", ""), i = "https://m.weibo.cn/sw.js", o = !1;
      n && (n.split(".")[0] > 1 || n.split(".")[1] >= 20) ? o || (o = !0,
      navigator.serviceWorker.register(i).then((function(e) {
          e.onupdatefound = function() {
              if (console.log("onupdatefound"),
              navigator.serviceWorker.controller) {
                  console.log("检测到:");
                  var t = e.installing;
                  t.onstatechange = function() {
                      switch (t.state) {
                      case "installed":
                          window.__wb_performance_data.sw = 1,
                          console.log("[SW]: New content is available; please refresh.");
                          break;
                      case "redundant":
                          window.__wb_performance_data.sw = "redundant",
                          navigator.serviceWorker.controller.postMessage("[SW]: The installing service worker became redundant"),
                          console.error("[SW]: The installing service worker became redundant");
                          break;
                      default:
                      }
                  }
              }
          }
      }
      )).catch((function(e) {
          window.__wb_performance_data.sw = e.msg,
          navigator.serviceWorker.controller && navigator.serviceWorker.controller.postMessage("[SW]: Error during service worker registration: ".concat(e)),
          console.error("[SW]: Error during service worker registration:", e)
      }
      )),
      navigator.serviceWorker.onmessage = function(e) {
          var t = e.data;
          "UPDATE_FOUND" === t.command && console.log("[SW]: New cache is available; please refresh.")
      }
      ) : navigator.serviceWorker.getRegistration && navigator.serviceWorker.getRegistration(i).then((function(e) {
          e && e.unregister && e.unregister().then((function(e) {
              e ? console.log("[SW]: UnRegistration  succeeded.") : (navigator.serviceWorker.controller.postMessage("[SW]: UnRegistration failed."),
              console.error("[SW]: UnRegistration failed."))
          }
          ))
      }
      )).catch((function(e) {
          window.__wb_performance_data.sw = e.msg,
          navigator.serviceWorker.controller && navigator.serviceWorker.controller.postMessage("[SW]: UnRegistration failed with. ".concat(e)),
          console.error("[SW]: UnRegistration failed with. ".concat(e))
      }
      ));
      var r = 6e4
        , s = !0;
      window.addEventListener("beforeinstallprompt", (function(n) {
          if (a["a"].hasData("prompt_dismissed") && Date.now() - a["a"].getData("prompt_dismissed") < 216e5)
              n.preventDefault();
          else if (s) {
              e = n;
              var i = navigator.userAgent.toLowerCase().match(/chrom(e|ium)\/([0-9]+)/)
                , o = i && i.length >= 2 ? parseInt(i[2], 10) : null;
              o && e.prompt && (n.preventDefault(),
              s = !1,
              setTimeout((function() {
                  o <= 67 ? e.prompt() : document.addEventListener("click", t)
              }
              ), r))
          }
      }
      ))
  }
}        ));
