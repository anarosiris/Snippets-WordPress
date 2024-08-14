Calcular el tiempo de lectura de un post en WP

Para crear un shortcode que calcule y muestre el tiempo de lectura de un post en WordPress, puedes seguir estos pasos. Este shortcode te permitirá insertar el cálculo del tiempo de lectura en cualquier lugar del contenido del post o en las plantillas del tema.

### Código del Shortcode para Calcular el Tiempo de Lectura

```php
function shortcode_tiempo_lectura() {
    global $post;

    // Velocidad de lectura promedio en palabras por minuto
    $velocidad_lectura = 200;

    // Obtener el contenido del post actual
    $contenido_post = $post->post_content;

    // Contar las palabras en el contenido del post
    $cantidad_palabras = str_word_count(strip_tags($contenido_post));

    // Calcular el tiempo de lectura en minutos
    $tiempo_lectura = ceil($cantidad_palabras / $velocidad_lectura);

    // Devolver el tiempo de lectura en un formato legible
    return '<p>Tiempo de lectura: ' . $tiempo_lectura . ' minutos</p>';
}

// Registrar el shortcode en WordPress
add_shortcode('tiempo_lectura', 'shortcode_tiempo_lectura');
```

### Explicación del Código

1. **Función `shortcode_tiempo_lectura()`**:
   - **`global $post;`**: Accede al contenido del post actual.
   - **Velocidad de lectura**: Establecida en 200 palabras por minuto.
   - **Conteo de palabras**: Utiliza `str_word_count(strip_tags($contenido_post))` para contar las palabras, eliminando las etiquetas HTML.
   - **Cálculo del tiempo**: Divide el número de palabras por la velocidad de lectura y redondea hacia arriba con `ceil()`.
   - **Devolución del resultado**: Devuelve el tiempo de lectura en un párrafo HTML.

2. **Registro del Shortcode**:
   - **`add_shortcode('tiempo_lectura', 'shortcode_tiempo_lectura');`**: Registra el shortcode `[tiempo_lectura]`, que ejecuta la función `shortcode_tiempo_lectura`.

### Cómo Usar el Shortcode

- **En el Editor de Post**:  
  Puedes añadir `[tiempo_lectura]` en cualquier parte del contenido de tu post, y WordPress lo reemplazará con el tiempo estimado de lectura.

- **En una Plantilla de Tema**:  
  Si deseas insertar el tiempo de lectura directamente en la plantilla de tu tema, puedes usar el siguiente código PHP:

  ```php
  echo do_shortcode('[tiempo_lectura]');
  ```

### Ejemplo de Uso en Plantilla

Supongamos que deseas mostrar el tiempo de lectura en la plantilla de un post, podrías colocar el siguiente código en el archivo `single.php` o en cualquier otra plantilla de tu tema:

```php
<div class="contenido-post">
    <?php the_content(); ?>
    <?php echo do_shortcode('[tiempo_lectura]'); ?>
</div>
```

Este código mostrará el contenido del post seguido del tiempo estimado de lectura. Puedes colocarlo en cualquier parte de la plantilla según tus necesidades de diseño.

Este enfoque te permite fácilmente agregar y gestionar el cálculo del tiempo de lectura en tus posts, ofreciendo una mejor experiencia al usuario al proporcionar información adicional sobre el contenido.