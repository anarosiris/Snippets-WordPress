Snippet para generar índice o tabla de contenido AUTOMÁTICO en un Post o entrada de WordPress

Crear un índice de contenidos en WordPress que cumpla con tus requisitos es una excelente manera de mejorar la usabilidad y la experiencia del usuario.

### Código índice o tabla de contenido AUTOMÁTICO

```php

function generar_indice_contenidos($content) {
    // Verificar si el campo ACF 'indice_contenidos_entrada' está marcado como verdadero
    if (get_field('indice_contenidos_entrada') === true) {

        // Buscar todos los H1, H2 y H3 en el contenido del post
        preg_match_all('/<h([1-3])>(.*?)<\/h[1-3]>/', $content, $matches, PREG_SET_ORDER);

        // Verificar si hay al menos un H1, H2 o H3
        if (count($matches) > 0) {
            $indice = '<div class="indice-contenidos-wrapper">';
            $indice .= '<button class="toggle-indice">Mostrar/Ocultar Índice</button>';
            $indice .= '<ul class="indice-contenidos" style="display:none;">'; // Lista sin numeración

            $num_h1 = 0; // Contador para H1
            $num_h2 = 0; // Contador para H2 dentro de cada H1
            $num_h3 = 0; // Contador para H3 dentro de cada H2

            foreach ($matches as $match) {
                if ($match[1] == '1') {
                    $num_h1++;
                    $num_h2 = 0;
                    $num_h3 = 0;
                    $indice .= '<li><a href="#h1-' . $num_h1 . '">' . $match[2] . '</a></li>';
                    $content = str_replace($match[0], '<h1 id="h1-' . $num_h1 . '">' . $match[2] . '</h1>', $content);
                } elseif ($match[1] == '2') {
                    $num_h2++;
                    $num_h3 = 0;
                    $indice .= '<li class="sub-item"><a href="#h1-' . $num_h1 . '-h2-' . $num_h2 . '">' . $match[2] . '</a></li>';
                    $content = str_replace($match[0], '<h2 id="h1-' . $num_h1 . '-h2-' . $num_h2 . '">' . $match[2] . '</h2>', $content);
                } elseif ($match[1] == '3') {
                    $num_h3++;
                    $indice .= '<li class="sub-item sub-item-h3"><a href="#h1-' . $num_h1 . '-h2-' . $num_h2 . '-h3-' . $num_h3 . '">' . $match[2] . '</a></li>';
                    $content = str_replace($match[0], '<h3 id="h1-' . $num_h1 . '-h2-' . $num_h2 . '-h3-' . $num_h3 . '">' . $match[2] . '</h3>', $content);
                }
            }

            $indice .= '</ul>'; // Lista sin numeración
            $indice .= '</div>';

            // Insertar el índice al inicio del contenido
            $content = $indice . $content;
        }
    }

    return $content;
}
add_filter('the_content', 'generar_indice_contenidos');

function estilos_y_scripts_indice_contenidos() {
    ?>
    <style>
        .indice-contenidos-wrapper {
            margin-top: 30px;
			margin-bottom: 30px;
			width: 100%; /* Ajusta el ancho según tus necesidades */
			max-width: 800px; /* Ancho máximo para mantener el diseño en pantallas grandes */
		
			
        }
        .toggle-indice {
            background-color: #0073aa;
            color: #fff;
            padding: 10px 15px;
            border: none;
            cursor: pointer;
            border-radius: 15px;
            margin-bottom: 0px;
        }
        .toggle-indice:hover {
            background-color: #005177;
        }
        .indice-contenidos {
            list-style-type: auto; /* Elimina la numeración */
            margin-left: 10px; /* Margen ajustado */
			background-color: #f5f5f5;
			padding: 20px;
			border-radius: 15px;
			font-weight: 300;
			line-height: 30px;

        }
        .indice-contenidos .sub-item {
            margin-left: 20px; /* Margen igual para los elementos secundarios */
        }
        .indice-contenidos .sub-item-h3 {
            margin-left: 40px; /* Indentación adicional para H3 */
        }
    </style>
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            const toggleButton = document.querySelector('.toggle-indice');
            const indice = document.querySelector('.indice-contenidos');

            if (toggleButton && indice) {
                toggleButton.addEventListener('click', function() {
                    if (indice.style.display === "none") {
                        indice.style.display = "block";
                    } else {
                        indice.style.display = "none";
                    }
                });
            }
        });
    </script>
    <?php
}
add_action('wp_head', 'estilos_y_scripts_indice_contenidos');

```


### Explicación del Código

1. **Verificación del Campo ACF (`indice_contenidos_entrada`)**:
   - La función `get_field('indice_contenidos_entrada')` verifica si el campo ACF está marcado como verdadero (es decir, si el índice debe mostrarse).

2. **Extracción de Títulos (`H1` y `H2`)**:
   - `preg_match_all('/<h([1-2])>(.*?)<\/h[1-2]>/')` busca todos los títulos `H1` y `H2` en el contenido.
   - El código numera los títulos para crear enlaces únicos y reemplaza los títulos originales con versiones que incluyen un `id` único.

3. **Construcción del Índice**:
   - Se construye una lista numerada (`<ol>`) que muestra los títulos `H1` y `H2`, con subniveles para los `H2`.
   - Cada enlace en la lista lleva al correspondiente título en el contenido.

4. **Inserción del Índice**:
   - El índice se inserta al inicio del contenido del post.

5. **Estilos y Scripts**:
   - **CSS**: Estilos para el botón de mostrar/ocultar el índice y la lista numerada.
   - **JavaScript**: Controla el comportamiento del botón para plegar y desplegar el índice.

6. **Optimización**:
   - Se utiliza `document.addEventListener('DOMContentLoaded')` para asegurarse de que el script se ejecute solo después de que el DOM esté completamente cargado.
   - El código solo se ejecuta si el índice debe mostrarse, lo que minimiza el impacto en el rendimiento.

### Uso

- **Condicional**: El índice de contenidos solo aparecerá si el campo ACF `indice_contenidos_entrada` está marcado como verdadero en la edición del post.
- **Inserción en el Post**: El índice se agrega automáticamente al inicio del contenido del post si se cumplen las condiciones.

Este código es eficiente, fácil de mantener y asegura que el índice solo se muestre cuando sea necesario, minimizando cualquier impacto en la velocidad de carga de la página.