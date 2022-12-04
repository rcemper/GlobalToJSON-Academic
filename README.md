# GlobalToJSON-Academic
This package offers a utility to load a Global into JSON object and to create a    
Global from this type of JSON object. ***Academic*** refers to the structure created.    
Each logical node of the Global is presented separately with all its descendants    
even if they don't contain any stored data.   

<img width="80%" src="https://raw.githubusercontent.com/rcemper/GlobalToJSON-Academic/master/Globals.png">    

## Prerequisites
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.
## Installation 
Clone/git pull the repo into any local directory
```
git clone https://github.com/rcemper/GlobalToJSON-Academic.git
```
Run the IRIS container with your project: 
```
docker-compose up -d --build
```
## How to Test it
This is the pre-loaded Global **^dc.MultiD** for testing.
![](https://raw.githubusercontent.com/rcemper/GlobalToJSON-Academic/master/Global.JPG)

Open IRIS terminal
```
$ docker-compose exec iris iris session iris
USER>

USER>; generate JSON object from Global

USER>set json=##class(dc.GblToJSON.A).do("^dc.MultiD")

USER>zw json
json={"node":"^dc.MultiD","val":"5","sub":[{"node":"1","val":"$lb(\"Braam,Ted Q.
\",51353)","sub":[{"node":"mJSON","val":"{}"}]},{"node":"2","val":"$lb(\"Klingma
n,Uma C.\",62459)","sub":[{"node":"2","sub":[{"node":"Multi","sub":[{"node":"a",
"val":"1"},{"node":"rob","sub":[{"node":"1","val":"rcc"},{"node":"2","val":"2222
"}]}]}]},{"node":"Multi","sub":[{"node":"a","val":"1"},{"node":"rob","sub":[{"no
de":"1","val":"rcc"},{"node":"2","val":"2222"}]}]},{"node":"mJSON","val":"{\"A\"
:\"ahahah\",\"Rob\":\"VIP\",\"Rob2\":1111,\"Rob3\":true}"}]},{"node":"3","val":"
$lb(\"Goldman,Kenny H.\",45831)","sub":[{"node":"mJSON","val":"{}"}]},{"node":"4
","val":"$lb(\"\",\"\")","sub":[{"node":"mJSON","val":"{\"rcc\":122}"}]},{"node"
:"5","val":"$lb(\"\",\"\")","sub":[{"node":"mJSON","val":"{}"}]}]}  ; <DYNAMIC OBJECT>

USER>; this is rather hard to read and follow

USER>write $$Do^ZPretty(json)
```
![](https://raw.githubusercontent.com/rcemper/GlobalToJSON-Academic/master/ZPretty.gif)

Now we want to verify the load function.  
First we make a copy of our source and then delete the source   
After the load operation the source Global is completely restored    
```
USER>merge ^keep=^dc.MultiD  

USER>kill ^dc.MultiD

USER>set sc=##class(dc.GblToJSON.A).load(json)

USER>zw sc
sc=1

USER>zw ^dc.MultiD
^dc.MultiD=5
^dc.MultiD(1)=$lb("Braam,Ted Q.",51353)
^dc.MultiD(1,"mJSON")="{}"
^dc.MultiD(2)=$lb("Klingman,Uma C.",62459)
^dc.MultiD(2,2,"Multi","a")=1
^dc.MultiD(2,2,"Multi","rob",1)="rcc"
^dc.MultiD(2,2,"Multi","rob",2)=2222
^dc.MultiD(2,"Multi","a")=1
^dc.MultiD(2,"Multi","rob",1)="rcc"
^dc.MultiD(2,"Multi","rob",2)=2222
^dc.MultiD(2,"mJSON")="{""A"":""ahahah"",""Rob"":""VIP"",""Rob2"":1111,""Rob3"":true}"
^dc.MultiD(3)=$lb("Goldman,Kenny H.",45831)
^dc.MultiD(3,"mJSON")="{}"
^dc.MultiD(4)=$lb("","")
^dc.MultiD(4,"mJSON")="{""rcc"":122}"
^dc.MultiD(5)=$lb("","")
^dc.MultiD(5,"mJSON")="{}"

USER>
```
**q.a.d.**   

[Article in DC](https://community.intersystems.com/post/globaltojson-academic)

[Video](https://youtu.be/8Fz2537FHzc)
