# renderTable
Renderizador de tablas de datos para php-bootstrap-jsFramework

Tiene como fin poder crear tablas de datos a partir de un array de datos cargado desde una fuente de datos.

- [Inicialización de la Tabla](https://github.com/jsmorales/renderTable#inicialización-de-la-tabla)

- [Parámetros](https://github.com/jsmorales/renderTable#parámetros)
    - [arraydatos](https://github.com/jsmorales/renderTable#arraydatos)
    - [arraycampos](https://github.com/jsmorales/renderTable#array_campos)
        - [Tipos](https://github.com/jsmorales/renderTable#tipos-disponibles)
            - [strlen](https://github.com/jsmorales/renderTable#strlen)
            - [number_format](https://github.com/jsmorales/renderTable#number_format)
            - [percent](https://github.com/jsmorales/renderTable#percent)
   - [array_botones](https://github.com/jsmorales/renderTable#array_botones)
        - [Tipos](https://github.com/jsmorales/renderTable#tipos-de-botón-disponibles)
            - [editar](https://github.com/jsmorales/renderTable#editar)
            - [eliminar](https://github.com/jsmorales/renderTable#eliminar)
            - [descargar_1](https://github.com/jsmorales/renderTable#descargar_1)
            - [ver_docs](https://github.com/jsmorales/renderTable#ver_docs)
   - [array_opciones](https://github.com/jsmorales/renderTable#array_opciones)

- [Métodos](https://github.com/jsmorales/renderTable#métodos)
    - [render()](https://github.com/jsmorales/renderTable#render)
    - [render_blank()](https://github.com/jsmorales/renderTable#render_blank)
   

# Inicialización de la Tabla

En primer lugar se debe incluir la clase dentro del controlador:

```PHP
include_once 'helper_controller/render_table.php';

```
Se hace la instancia:

```PHP
$this->table_inst = new RenderTable($this->arrayDatos,$array_campos,$array_botones,$array_opciones);

```
# Parámetros:

## $arrayDatos
Es el array cargado de datos, ya se por DAO o por otro metodo de acceso de datos.

## $array_campos
Es un array cargado de datos manualmente, dice cuales campos queremos ver en nuestra tabla, van dentro de nombre:

```PHP
$array_campos = [
    			["nombre"=>"pkID"],
    			["nombre"=>"alias"],
    			["nombre"=>"nombre"],
    			["nombre"=>"apellido"],
    			["nombre"=>"nom_tipo"]
    		];
```
Para estos campos se puede necesitar una forma especial de visualizacion o formato, puede ser seteado en este array, van dentro de tipo, si no se define ningun tipo solo muestra el campo tal como viene de la consulta de datos:

```PHP
$array_campos = [
          ["nombre"=>"nombre"],
          ["nombre"=>"fechaIni"],
          ["nombre"=>"fechaFin"],
          [
            "nombre"=>"objeto",
            "tipo"=>"strlen",
            "len"=>60
          ],

          [
            "nombre"=>"total",
            "tipo"=>"number_format"
          ]
];
```
## Tipos Disponibles:

###### strlen
Limita la cantidad de caracteres que se verá en la tabla, viene acompañado de otro parámetro llamado **len** debe ser un entero, será la cantidad de caracteres que se puedan ver.

###### number_format
Muestra los campos de tipo dinero, por ahora solo con signo $.

###### percent
Muestra los campos de tipo porcentage con signo %.

## $array_botones
Este array nos permite definir las opciones del registro:

```PHP
$array_botones =[
            [
              "tipo"=>"editar",
              "nombre"=>"proyecto",
              "permiso"=>$edita,
            ],
            [
              "tipo"=>"eliminar",
              "nombre"=>"proyecto",
              "permiso"=>$elimina,
            ],
            [
              "tipo"=>"descargar_1",
              "nombre"=>"ruta",
            ],
            [
              "tipo"=>"ver_docs",
              "nombre"=>"ruta",
            ]
          ];
```
## Tipos de Botón Disponibles
Los tipo estan definidos por el framework:

Para editar,eliminar **nombre** es el nombre del módulo definido para jquerycontrollerv2.

Para editar,eliminar **permiso** es la variable definida de los permisos del framework.

###### editar
Muestra el boton con el lápiz de color amarillo, (warning). Abre modal cargando los datos para poderlos actualizar.
###### eliminar
Muestra el boton con la x de color rojo, (danger). Pide confirmación, eliminando el registro de la base de datos.
###### descargar_1
Muestra el boton de color verde para descargar archivo. El nombre es el campo en la base de datos que contiene el nombre del archivo.
###### ver_docs
Muestra el boton de color azul para visualizar archivo. El nombre es el campo en la base de datos que contiene el nombre del archivo. 

## $array_opciones
```PHP
$array_opciones = [
          "modulo"=>"proyecto",//nombre del modulo definido para jquerycontrollerV2
          "title"=>"Click Ver Detalles",//etiqueta html title
          "href"=>"detail_proyecto.php?id_proyecto=&filter_gastos=*&filter_documentos=*",
          "class"=>"detail"//clase que permite que añadir el evento jquery click
        ];
```
Permite que todo el **td** de la tabla sea un link al detalle de este registro en caso de tenerlo.

# Métodos:

## render()
Renderiza la tabla según los parámetros:

```PHP
  $this->table_inst->render();
```
## render_blank()
Renderiza los **td** sin nada dentro una sola vez, esto funciona para cuando la tabla no tiene datos y no dejarla sin un **tbody**
```PHP
  $this->table_inst->render_blank();
```


