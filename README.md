import os
import concurrent.futures

def descargar_sitio_web(url, destino):
    comando = f"wget -P {destino} {url}"
    os.system(comando)

def descargar_sitio_web_concurrente(url, destino, num_hilos):
    with concurrent.futures.ThreadPoolExecutor(max_workers=num_hilos) as executor:
        futures = []
        for _ in range(num_hilos):
            future = executor.submit(descargar_sitio_web, url, destino)
            futures.append(future)
        
        # Esperar a que se completen todas las descargas
        concurrent.futures.wait(futures)

# Ejemplo de uso

num_hilos = 322
url = "deamostwanted.info"  # Reemplaza con la URL o dirección IP correspondiente
destino = "/home/ubuntu/jhgjgjhghhjhgh"  # Reemplaza con la ruta de destino adecuada
descargar_sitio_web_concurrente(url, destino, num_hilos)
