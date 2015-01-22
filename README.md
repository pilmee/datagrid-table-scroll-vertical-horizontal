# Tabla "Datagrid de datos" con scroll VERTICAL y HORIZONTAL
Acontinuacion se presenta el diseño e implementacion de un datagrid de datos creado a partir de dos tablas (cabecera de datos y cuerpo de datos) en el cual se necesitaba colocar dos scrolls de desplazamiento (verticla y horizontal).

######Nota:
1. Se incluyo las liberias CSS de TwitterBootstrap solo para la presentacion.
2. La solucion no depende de la libreria TwitterBootstrap mencionada anteriormente.

######Compatiblidad:
* Es compatible con navegadores modernos (Chrome, Firefox, etc) y con internet explorer (version >= 9), aunque existe un defecto visual que sera correjido a la brevedad.


######Implementacion:
__HTML__
```html
<div class="grid" id="grid">
	<div class="head" id="grid-head">
		<table class="table">
			<thead>
				<tr>
					<th style="width: 10%">#</th>
					<th style="width: 30%">CABECERA 1</th>
					<th style="width: 40%">CABECERA 2</th>
					<th style="width: 10%">CABECERA 3</th>
					<th style="width: 10%">CABECERA 4</th>
				</tr>
			</thead>
		</table>
	</div>
	<div class="body" id="grid-body">
		<table class="table">
			<tbody>
				<tr>
					<td style="width: 10%">1</td>
					<td style="width: 30%">INFORMACION DE CABECERA 1</td>
					<td style="width: 40%">INFORMACION DE CABECERA 2</td>
					<td style="width: 10%">INFORMACION DE CABECERA 3</td>
					<td style="width: 10%">INFORMACION DE CABECERA 4</td>
				</tr>
				<tr>
				  ...
				</tr>
			</tbody>
		</table>
	</div>
</div>
```
> Definicion de la estructura HTML del grid la cual cuenta con dos tablas (una de cabecera y otra de cuerpo envueltas en un div padre)

__CSS__
```css
.grid{
	position:relative;
	width:600px;
	height:400px;
	overflow:auto;
	border:2px solid #ccc;
}
.grid .head{
	position:absolute;
	width:2000px;
	z-index: 9;
	background-color:#fff;
}
.grid table{
	margin-bottom:0;
}
.grid .body{
	position:relative;
	width:2000px;
}
```
> Clases CSS que le dan el alto y ancho del GRID asi como tambien el alto de la tabla contenida dentro del DIV#grid padre.

__JAVASCRIPT__
```javascript
var tableHeight;
var objTable = document.getElementById("grid-head");
if(objTable.offsetHeight)          { tableHeight=objTable.offsetHeight;}
else if(objTable.style.pixelHeight){ tableHeight=objTable.style.pixelHeight;}

document.getElementById("grid-body").style.marginTop = tableHeight + 'px';

document.getElementById("grid").addEventListener("scroll", function(e){
	objTable.style.top = this.scrollTop + 'px';
});
```
> En esta parte preguntamos en primer lugar por el alto de la cabecera y es que este alto es el margen supeior del cuerpo.
> Seguidamente asignamos una escucha al evento "scroll" para que actualize el valor top de la cabera que al ser absoluta tiene que reposicionarse segun sea el movimiento del scroll. 
