# Servidor de GTA 1000 para Render

Servidor WebSocket para una sala de hasta ocho jugadores. Sincroniza la posición de los jugadores a pie o en vehículo, el modo de vuelo y el piso del garaje. Cada cliente conserva su propia partida.

## Publicar en Render

1. Descomprime el ZIP y sube el contenido a la raíz de un repositorio Git. Deben quedar visibles `Dockerfile`, `render.yaml`, `project.godot`, `scripts/` y `scenes/`.
2. En Render, abre **New → Blueprint**, conecta ese repositorio y aplica `render.yaml`. También puedes crear un **Web Service** con runtime **Docker** desde el mismo repositorio.
3. En los logs busca `Ciudad Aurora escuchando WebSocket en el puerto 10000`.
4. Copia el dominio público asignado, por ejemplo `wss://gta1000-aurora.onrender.com`. En GTA 1000 abre **Multijugador por Internet**, pega la dirección, pulsa **Conectar** y elige **Entrar al mundo compartido**. Cada jugador usa la misma dirección. El servidor acepta conexiones públicas de clientes compatibles del juego.
5. Para comprobarlo, conecta dos dispositivos e inicia ambos en el mismo lugar de Ciudad Aurora. Mueve un jugador y observa el avatar en el otro dispositivo.

Render gestiona TLS en el dominio público. El proceso de Godot escucha en `0.0.0.0` y usa la variable `PORT`. El plan gratuito puede suspender el servicio durante periodos de inactividad. Si el primer intento caduca mientras arranca el contenedor, repite la conexión cuando el servicio esté activo.

## Prueba local

```sh
PORT=10000 godot --headless --path .
```

Con dos clientes locales usa `ws://127.0.0.1:10000`. Desde un equipo distinto en la misma red usa la IP del equipo servidor.
