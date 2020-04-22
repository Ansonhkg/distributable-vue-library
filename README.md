```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Project Foo</title>

    <!-- configure app -->
    <script src="https://unpkg.com/vue"></script>
    <script src="https://distributable.now.sh/configure.umd.min.js"></script>
    <link rel="stylesheet" href="https://distributable.now.sh/configure.css">

</head>
<body>
<h1>App</h1>
<p>
    Lorem ipsum, dolor sit amet consectetur adipisicing elit. Unde laborum fugit autem voluptas quo aperiam eaque voluptatibus, placeat vitae recusandae reiciendis quae corporis ipsa, blanditiis perferendis quos sed mollitia doloremque!
    Natus blanditiis molestias minima consectetur, distinctio reprehenderit et sit, nihil, illo mollitia possimus porro impedit aliquam nesciunt nostrum tempore? Asperiores at rerum commodi dignissimos officia! Eum cum voluptas eaque eos!
    Dolor, <button class="launch-conf-app" data="{site: 'Mayfair', floor: 1}">Go Configure</button> omnis aliquid? Sunt nemo delectus qui consequatur ab voluptatem ipsam! Dolorem non ducimus, nulla quia quaerat ipsa iusto voluptas. Ipsum soluta, consequuntur error ratione dolorem incidunt vero maxime ipsa!
    Aliquid praesentium, excepturi totam cupiditate animi dignissimos eum. Non labore dignissimos nesciunt maxime illum eius ipsam. Voluptate, ullam libero? Cum reprehenderit nam odit tempore cupiditate repudiandae praesentium. Quia, expedita eum!
    Voluptates minima dolorem veniam vitae eum nemo quaerat nulla quae enim. Totam libero amet animi explicabo aut tempora, quis voluptate. Iste fugiat laborum sequi illum? Totam magnam mollitia doloribus molestiae.
</p>

<!-- place this before </body> -->
<div id="configure-app">
    <configure-app></configure-app>
</div>

<script>
    const vm = new Vue({
      components: {
        configureApp: configure
      }
    }).$mount('#configure-app');

    const configureApp = vm.$options.components.configureApp.methods;
</script>
</body>
</html>
```