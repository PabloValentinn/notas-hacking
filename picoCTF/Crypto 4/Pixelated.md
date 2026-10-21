

## DESCRIPCION
- I have these 2 images, can you make a flag out of them? [scrambled1.png](https://challenge-files.cylabacademy.net/library/5d582e313e019eefa2385b079dac13cc187060301fb28ae53d6cdeb2d5ac2af2/scrambled1.png) [scrambled2.png](https://challenge-files.cylabacademy.net/library/5d582e313e019eefa2385b079dac13cc187060301fb28ae53d6cdeb2d5ac2af2/scrambled2.png)

## SOLUCION
```

- Se analizaron las dos imágenes proporcionadas (`scrambled1.png` y `scrambled2.png`), las cuales a simple vista contenían únicamente patrones de ruido estático RGB aparentemente aleatorio.
    
- **Identificación de la técnica:** La premisa del desafío corresponde a un esquema clásico de **Criptografía Visual** (Visual Cryptography). En este método, una imagen secreta se divide en dos o más capas compartidas (_shares_). De forma aislada, cada imagen no contiene información interpretable, pero al superponerlas matemáticamente, los valores de los píxeles interfieren y revelan el mensaje subyacente.
    
- Se implementó un script en Python utilizando las librerías `PIL` (Pillow) y `numpy` para cargar ambas imágenes como matrices bidimensionales y realizar una suma aritmética de los valores de sus canales de color píxel por píxel:
    
    Python
    
    ```
    import numpy as np
    from PIL import Image
    
    # Carga de las matrices de píxeles
    img1 = np.asarray(Image.open("scrambled1.png"))
    img2 = np.asarray(Image.open("scrambled2.png"))
    
    # Suma aritmética de canales (los valores que superan 255 se saturan/desbordan)
    combined = img1.copy() + img2.copy()
    
    # Reconstrucción y guardado de la imagen resultante
    result = Image.fromarray(combined)
    result.save("flag_revelada.png")
    
```

## NOTAS ADICIONALES
- Criptografía Visual y Esteganografía por Superposición: Introducida originalmente por Moni Naor y Adi Shamir en 1994, la criptografía visual aprovecha la percepción humana para descifrar secretos sin requerir cómputo criptográfico formal una vez que las capas se alinean. En entornos digitales, las operaciones de combinación más habituales entre capas son la suma aditiva (ADD) y la disyunción exclusiva (XOR). Herramientas gráficas como `Stegsolve` (mediante su función *Image Combiner*) o scripts vectorizados con `numpy` permiten iterar rápidamente entre operaciones lógicas para hallar el modo exacto de revelado.

## REFERENCIAS
- Reto original: picoCTF 2021 - Categoría: Cryptography (Medium)[cite: 10]. - Conceptos aplicados: Criptografía Visual, Manipulación de Matrices de Imágenes con NumPy/Pillow, Operación Aditiva de Píxeles (Image Overlay/ADD).