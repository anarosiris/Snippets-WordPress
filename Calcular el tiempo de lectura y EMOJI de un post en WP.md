
Para sustituir la frase "Tiempo de lectura:" por un emoji de libro, puedes actualizar el shortcode de la siguiente manera:

### Código del Shortcode con Emoji de Libro

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

    // Devolver el tiempo de lectura con un emoji de libro
    return '<p>📚 ' . $tiempo_lectura . ' minutos</p>';
}

// Registrar el shortcode en WordPress
add_shortcode('tiempo_lectura', 'shortcode_tiempo_lectura');
```

### Explicación de la Actualización

- **`📚`**: Este es el emoji de libro que sustituye la frase "Tiempo de lectura:". Ahora, el shortcode mostrará el emoji seguido del tiempo de lectura en minutos.

### Ejemplo de Uso en Plantilla

Si deseas mostrar el tiempo de lectura con el emoji de libro en la plantilla de un post, puedes colocar el siguiente código en tu archivo `single.php` o en cualquier otra plantilla de tu tema:

```php
<div class="contenido-post">
    <?php the_content(); ?>
    <?php echo do_shortcode('[tiempo_lectura]'); ?>
</div>
```

Este código agregará el tiempo de lectura justo después del contenido del post, precedido por el emoji de un libro.
