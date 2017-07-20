#深入理解Android网络编程  

##第一章 ：网络编程概要  
Uir.parse()//方法返回一个URL类型，Intent.ACTION\_VIEW调用系统浏览器打开指定网页  
  
        Uri uri = Uri.parse("http://translate.google.cn/");
        Intent intent = new Intent(Intent.ACTION_VIEW, uri);
        startActivity(intent);
<center>![](http://i.imgur.com/oc7Kw19.jpg)</center>  

        WebView webView = (WebView) findViewById(R.id.webView1);
        webView.loadUrl("http://www.baidu.com/");
        webView.setWebViewClient(new WebViewClient() {
            public boolean shouldOverrideUrlLoading(WebView view, String request) {
                view.loadUrl(request);
                return true;
            }
        });  
  

