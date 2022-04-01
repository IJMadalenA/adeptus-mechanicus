# Regular Expression.



<table>
   <thead>
      <tr>
         <th>Simbolo</th>
         <th>Significado</th>
      </tr>
   </thead>
   <tbody>
       <tr>
      	<td>^</td>
        <td>Coincide con el inicio del texto.</td>
       </tr>
       <tr>
      	<td>$</td>
        <td>Coincide con el fin del texto.</td>
       </tr>
       <tr>
       	<td>\d</td>
           <td>Coincide con un dígito (0, 1, 2, ...9)</td>
       </tr>
       <tr>
       	<td>\w</td>
           <td>Coincide con un caracter de palabra, ej. cualquier caracter del alfabeto en mayúscula o minúscula, dígito o guión bajo.</td>
       </tr>
       <tr>
       	<td>+</td>
           <td>Coincida con uno o más caracteres de precedente. Por ejemplo, para coincidir con uno o más dígitos usarías \d+. Para concidir con uno o más caracteres "a", podrías usar a+</td>
       </tr>
       <tr>
       	<td>*</td>
           <td>Concide con cero o más caracteres del precedente. Por ejemplo, para coincidir con nada o una palabra podrías usar \w*</td>
       </tr>
       <tr>
       	<td>()</td>
           <td>Captura la parte del patrón dentro de los paréntesis. Todos los calores capturados serán enviados a la vista como parámetros sin nombre (si se captura múltiples patrones, los parámetros  asociados serán enviados en el órden den que fueron declaradas las capturas).</td>
       </tr>
       <tr>
       	<td>(?<name>...)</td>
            <td>Captura el patrón (indicado por ...) como una variable con nombre (en este caso "name"). Los valores capturados se envían a la vista con el nombre especificado. Tu vista debe, por tanto, ¡declarar n argumento con el mismo nombre!</td>
       </tr>
       <tr>
       	<td>[]</td>
           <td>Concide con un caracter del conjunto. Por ejemplo, [abc] coincidirá con 'a' o 'b' o 'c'. [-\w] coincidirá con el caracter ' - ' o con cualquier letra.</td>
       </tr>
   </tbody>
</table>



