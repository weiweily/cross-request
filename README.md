### A chrome extension that gives the html page cross-domain request capability.
### 一个赋予html页面跨域请求能力的chrome扩展

https://chrome.google.com/webstore/detail/cross-request/cmnlfmgbjmaciiopcgodlhpiklaghbok?hl=en-US

### Usage
方式一：
在html页面添加 id="cross-request-sign" dom元素
方式二：
点击右上角yapi扩展，添加允许跨域的页面domain



### Code Example
```
<html>

<body>
    <h1 id="cross-request-sign">CrossRequest</h1>
    <input id="file" type="file" name="file" />
    <button id="upload">upload</button>
    <script>
        setTimeout(run, 1000)
          function run () {
            window.crossRequest({
                url: 'http://caibaojian.com/ajax-jsonp.html',
                method: 'GET',
                query: {
                    a: 1
                },
                success: function (res, header) {
                    console.log(header)
                }
            })


            //test get
            window.crossRequest({
                url: 'http://127.0.0.1:3000/api',
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                data: {
                    a: 1,
                    b: 2,
                    c: {
                        t: 1
                    }
                },
                success: function (res) {
                    console.log(arguments)
                }
            })

            //test error get
            window.crossRequest({
                url: 'http://127.0.0.1:3000/error_get',
                method: 'GET',
                error: function (err, header) {
                    console.log(err)
                }
            })

            //test form-data upload
            var file = document.getElementById('file');
            document.getElementById('upload').addEventListener('click', function () {
                window.crossRequest({
                    url: 'http://127.0.0.1:8081/upload',
                    method: 'POST',
                    data: {
                        name: 'hello',
                        id: '19'
                    },
                    files: {
                        file: 'file'
                    },
                    success: function (res) {
                        alert(res)
                    }
                })

            })

            //test single-upload
            document.getElementById('upload').addEventListener('click', function () {
                window.crossRequest({
                    url: 'http://127.0.0.1:8081/upload/single',
                    method: 'POST',
                    file: 'file',
                    success: function (res) {
                        alert(res)
                    }
                })

            })
        }
    </script>


</body>

</html>

```