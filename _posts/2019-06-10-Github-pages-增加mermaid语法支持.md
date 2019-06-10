---
layout: page
title: Github mermaid支持
---

github pages 不支持mermaid语法，很不方便，于是各种google，把这个语法支持放进去。

首先我们在文章开头配置是否开启mermaid支持，这样可以不必每次都加载mermaid组件，提升网速。比如我这里是这样写的：

```
---
layout: post
title: Github mermaid支持
mermaid: true
---
```



然后我们在网页加载的时候去渲染mermaid流程图就好了。我把以下代码放到我的仓库下的`_includes/footer-scripts.html`里面：

```js
{\% if page.mermaid \%}
      <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mermaid/8.0.0/mermaid.min.js"></script>
      <script>
          var config = {
              startOnLoad:true,
              flowchart:{
                  useMaxWidth:false,
                  htmlLabels:true
              }
          };
          mermaid.initialize(config);
          $(function(){
              var elements = document.getElementsByClassName("language-mermaid");
              for (var i = elements.length; i--;) {
                  element = elements[i];
                  var graphDefinition = element.innerText;
                  if (graphDefinition) {
                      var svg = mermaid.render('ha_mermaid_' + i, graphDefinition, function(svg){});
                      if (svg) {
                          var svgElement = document.createElement('div');
                          preNode = element.parentNode;
                          svgElement.innerHTML = svg;
                          svgElement.setAttribute('class', 'mermaid');
                          svgElement.setAttribute('data-processed', 'true');
                          preNode.parentNode.replaceChild(svgElement, preNode);
                      }
                  }
              }
          });
      </script>
{\% endif \%}
```

**注意: 上文中 {\% \%} 需要把 \ 去掉，因为写文章不加 \ 的话这句话就被 jekyll 当做语法使用了**



然后对于mermaid的各种图就可以支持了，mermaid语法详情请查看 [官方文档](https://mermaidjs.github.io/)

