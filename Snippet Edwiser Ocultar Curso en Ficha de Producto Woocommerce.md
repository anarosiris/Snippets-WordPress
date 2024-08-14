Snippet para WP donde este se oculte de la ficha de producto de Woocommerce:  <div class="wi-asso-courses-wrapper">
				<h5>Associated Courses</h5>

					<ul class="bridge-woo-available-courses">
						<li>
					<a href="https://dev.elearningfacil.com/courses/guia-de-instalacion-del-pack-fundae-para-moodle/" target="_blank">Guía de Instalación del Pack FUNDAE para Moodle</a>
									</li>
					</ul>
				</div>

Para ocultar un bloque de HTML específico como el que mencionas (`<div class="wi-asso-courses-wrapper">`) en la ficha de producto de WooCommerce, puedes utilizar un snippet de código en tu tema hijo o en un plugin de funcionalidades personalizadas.

### Snippet de Código para Ocultar el Div en la Ficha de Producto de WooCommerce

```php
function ocultar_associated_courses_div() {
    if (is_product()) {
        ?>
        <style>
            .wi-asso-courses-wrapper {
                display: none !important;
            }
        </style>
        <?php
    }
}
add_action('wp_head', 'ocultar_associated_courses_div');
```

### Explicación del Código

1. **`is_product()`**: Esta función verifica si estás en una ficha de producto de WooCommerce. Si es así, el código dentro del bloque se ejecutará.

2. **`<style>`**: Se inserta un bloque de estilo directamente en el `<head>` de la página.

3. **`.wi-asso-courses-wrapper { display: none !important; }`**: Este CSS oculta el div con la clase `wi-asso-courses-wrapper` en la ficha de producto, utilizando `display: none !important;` para asegurarse de que el estilo sea prioritario sobre otros estilos que puedan aplicarse.

4. **`add_action('wp_head', 'ocultar_associated_courses_div');`**: El código se engancha en el hook `wp_head`, lo que garantiza que el estilo se agregue al `<head>` de la página cuando se carga una ficha de producto.

### Cómo Usar el Snippet

1. **Agregar el Snippet a tu Tema Hijo**:  
   Copia el código y pégalo en el archivo `functions.php` de tu tema hijo.

2. **Usar un Plugin de Snippets**:  
   Si prefieres no editar el `functions.php`, puedes usar un plugin como [Code Snippets](https://es.wordpress.org/plugins/code-snippets/) para agregar y gestionar snippets de código.

Este snippet ocultará el div específico de las fichas de producto en WooCommerce, logrando que el bloque no se muestre en la página del producto.
