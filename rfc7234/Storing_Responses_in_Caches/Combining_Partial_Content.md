如果连接过早关闭或如果请求使用了一个或多个Range，响应可能只转移一部分表示。在几次这样的转移后，缓存可能已经接收到一些相同表示的范围。缓存**可以**将这些范围组成成一个存储响应，然后使用哪个响应来满足后续请求，如果他们都共享相同的强校验器并且缓存符合RFC7233中4.3节的客户端要求。

当将一个或多个已存储的响应组成新响应时，缓存**必须**：

- 用警告代码1xx删除存储的响应中的任何警告头字段（5.5节）；
- 在warn-code 2xx中保留存储的响应中的任何Warning头域; 并且，
- 使用在新响应中提供的其他头字段，除了Content-Range，来取代所有已存储响应中对应头字段的实例。