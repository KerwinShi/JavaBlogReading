@RequestParam   
@RequestBody  
常见的后端接受前端请求的参数的注解  

@RequestParam接收的参数是来自HTTP***请求体或请求url***  
```
required 表示是否必须，默认为 true，必须。
defaultValue 可设置请求参数的默认值。
value 为接收url的参数名（相当于key值）。
```  
处理 Content-Type 为 application/x-www-form-urlencoded 编码的内容  

问题：  
无法批量处理数据，为了可以批量处理，就想到了利用json格式进行传递参数  

but，事情不简单，@RequestParam接收json格式参数，不友好，可以，但是麻烦  

@RequestBody对于json格式参数是友好的，一般用于处理非 Content-Type: application/x-www-form-urlencoded编码格式的数据，比如：application/json、application/xml等类型的数据。  

POST请求  
@RequestBody --> JSON字符串部分  
@RequestParam --> 请求参数部分    

GET请求  
GET请求中不可以使用@RequestBody  
@RequestParam --> 在url中的?后面添加参数




