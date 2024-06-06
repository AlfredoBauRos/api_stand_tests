# Proyecto de Pruebas positivas y negativas para la Creación de Usuarios

Este proyecto consta de pruebas automatizadas para verificar el correcto funcionamiento del parámetro `firstName` al crear un/a usuario/a en un servicio web. Las pruebas se realizan utilizando `pytest` y `requests`.

## Requisitos

- `Python 3.6 o superior`
- `pytest`
- `requests`

## Instalación

1. Clona el repositorio en tu máquina local:

   ```sh
   git clone <URL_del_repositorio>
   cd <nombre_del_repositorio>

## Crea un entorno virtual
* -inicia PyCharm.
* -Selecciona "New Project" para crear un nuevo proyecto.
* -Selecciona la configuración del proyecto.
* -Lenguaje. Selecciona Pure Python en el menú de la izquierda.
* -Identifica la ruta de tu proyecto: El nombre del último directorio es el nombre de tu proyecto.
* -Selecciona "New Virtualenv using" (Nuevo uso de Virtualenv) y luego elige Virtualenv en la lista desplegable.

## Instalar los paquetes

    pip install pytest requests


## Estructura del Proyecto

* data.py: Contiene los datos necesarios para las solicitudes y encabezados.
* configuration.py: Define las constantes de configuración, como las URL de servicio y las rutas de la API.
* sender_stand_request.py: Contiene funciones para enviar solicitudes HTTP al servicio web.
* create_user_test.py: Contiene las pruebas automatizadas para el parámetro firstName.

## Ejecución de Pruebas

    pytest create_user_test.py

ejecuta todas las pruebas, utiliza el siguiente comando en la terminal:

## Descripción de las Pruebas
Pruebas Positivas

Prueba 1: Creación de un/a usuario/a con un firstName que contiene dos caracteres.

    def test_create_user_2_letter_in_first_name_get_success_response():
    positive_assert("Aa")

Prueba 2: Creación de un/a usuario/a con un firstName que contiene quince caracteres.

    def test_create_user_15_letter_in_first_name_get_success_response():
    positive_assert("Aaaaaaaaaaaaaaa")

## Pruebas Negativas


Prueba 3: Creación de un/a usuario/a con un firstName que contiene un carácter.

    def test_create_user_1_letter_in_first_name_get_error_response():
    negative_assert_symbol("A")


Prueba 4: Creación de un/a usuario/a con un firstName que contiene dieciséis caracteres.

    def test_create_user_16_letter_in_first_name_get_error_response():
    negative_assert_symbol("Aaaaaaaaaaaaaaaa")


Prueba 5: Creación de un/a usuario/a con un firstName que contiene espacios.

    def test_create_user_has_space_in_first_name_get_error_response():
    negative_assert_symbol("A Aaa")


Prueba 6: Creación de un/a usuario/a con un firstName que contiene caracteres especiales.

    def test_create_user_has_special_symbol_in_first_name_get_error_response():
    negative_assert_symbol("\"№%@\",")


Prueba 7: Creación de un/a usuario/a con un firstName que contiene números.

    def test_create_user_has_number_in_first_name_get_error_response():
    negative_assert_symbol("123")


Prueba 8: Creación de un/a usuario/a sin el parámetro firstName.

    def test_create_user_no_first_name_get_error_response():
    user_body = data.user_body.copy()
    user_body.pop("firstName")
    negative_assert_no_firstname(user_body)


Prueba 9: Creación de un/a usuario/a con un firstName vacío.

    def test_create_user_empty_first_name_get_error_response():
    user_body = get_user_body("")
    negative_assert_no_firstname(user_body)

Prueba 10: Creación de un/a usuario/a con un firstName de tipo numérico.

    def test_create_user_number_type_first_name_get_error_response():
    user_body = get_user_body(12)
    response = sender_stand_request.post_new_user(user_body)
    assert response.status_code == 400