<h1>PASOS PARA DEJAR UN SERVIDOR FÍSICO DE LINUX OPTIMO PARA TRABAJAR CON WORDPRESS Y MOODLE</h1>

<H2>INTALACIONES Y CONFIGURACIONES</H2>
<ol>
<li>
    <h3>EXTENSIONES A INSTALAR PARA WORDPRESS Y MOODLE</h3>
        <h4>Extensiones de Moodle</h4>
        <ul>
            <ol>
                <h5>Extensión SODIUM de PHP</h5>
            </ol>
            <ol>
                <h5>Extensión EXIF de PHP</h5>
            </ol>
        </ul>
        <h4>Extensiones de Wordpress</h4>
        <ul>
            <ol>
                <h5>Extensión IMAGICK de PHP</h5>
            </ol>
        </ul>
</li>
<li>
    <h3>DIRECTIVAS DE PHP Y NGINX</h3>
        <h4>Directivas de PHP</h4>
        <ul>
            <ol>
                <h5><b>post_max_size: </b>10G</h5>
            </ol>
            <ol>
                <h5><b>max_input_time: </b>-1</h5>
                <p><mark>con -1 el max_input_time es ilimitado</mark></p>
            </ol>
            <ol>
                <h5><b>max_input_vars: </b>10000</h5>
            </ol>
            <ol>
                <h5><b>upload_max_filesize: </b>10G</h5>
            </ol>
            <ol>
                <h5><b>memory_limit: </b>1024M</h5>
            </ol>
            <ol>
                <h5><b>max_execution_time: </b>0</h5>
                <p><mark>con 0 el max_execution_time es ilimitado</mark></p>
            </ol>
        </ul>
        <h4>Directivas de NGINX</h4>
        <p><mark>Sino se modifica la directiva NGINX, no hace efecto las modificaciones de las directivas PHP</mark></p>
        <ul>
            <ol>
                <h5>client_max_body_size: 5G</h5>
            </ol>
        </ul>
</li>
<li>
    <h3>ERRORES FRECUENTES AL INSTALAR LINUX SERVER</h3>
    <h4>Bases de datos phpMyAdmin y carga de archivo SQL </h4>
    <p>Después de haber aplicado el cambio a las directivas aún puede dar error de timeout al momento de importar base de datos, esto se soluciona <mark>agregando dentro del <b>vhost de phpMyAdmin y nginx.conf </b> los parámetros para que los timeouts sean más altos[1] y PHP-FPM tenga el tiempo para procesar la carga</mark>, para ello se modifica lo siguiente:</p>
    <ol>
        <h5><li>proxy_connect_timeout 1200s;</li></h5>
        <h5><li>proxy_send_timeout 1200s;</li></h5>
        <h5><li>proxy_read_timeout 1200s;</li></h5>
        <h5><li>fastcgi_send_timeout 1200s;</li></h5>
        <h5><li>fastcgi_read_timeout 1200s;</li></h5>
    </ol>
    <h4>Error de timeout exclusivo de phpMyadmin</h4>
    <p>Es posible que si la base de datos es muy grande aún surjan nuevos errores de timeout al importar una base de datos. En ese caso se debería <mark><b></b> hacer la siguiente configuración para tener el timeout ilimitado:</mark></p>
    <ol>
    <h5><li>[root@1273540-app10 phpMyAdmin]# tail -3 config.inc.php</li></h5>
    <p>//ADDED TO AVOID TIMEOUT</p>
    <h5><li>$cfg['ExecTimeLimit'] = 0; </li></h5>
    </ol>


</li>
<li>
    <h3>PERMISOS DE USUARIO</h3>
</li>
<li>

</li>
<li>

</li>

</ol>