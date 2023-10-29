***Rule of thumb***
if you are using exchange.out you must copy the exchange.in headers across unless you have a really good reason not to...

Ex: 

```
@Override
    protected Processor createExceptionProcessor() {
        return new Processor() {
            
            @Override
            public void process(Exchange exchange) throws Exception {
                exchange.getOut().setHeaders(exchange.getIn().getHeaders());
                exchange.getOut().setHeader(Exchange.HTTP_RESPONSE_CODE, 500);

                exchange.getOut().setBody(null);
                
                ApiProxyRouteUtil.cleanExchangeHeaders(exchange);
            }
        };
    }
```
