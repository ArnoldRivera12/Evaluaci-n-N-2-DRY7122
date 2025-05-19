# Evaluaci-n-N-2-DRY7122
Arnold Rivera, Matias Chacon

import requests

API_KEY = "NC-50-061fb2f8637048f8a982-nbi"

def obtener_datos_viaje(origen, destino):
    url = f"https://graphhopper.com/api/1/route"
    params = {
        "point": [origen, destino],
        "vehicle": "car",
        "locale": "es",
        "calc_points": "false",
        "key": API_KEY
    }

    response = requests.get(url, params=params)
    if response.status_code == 200:
        datos = response.json()
        distancia_km = datos["paths"][0]["distance"] / 1000
        duracion_segundos = datos["paths"][0]["time"] / 1000
        horas = int(duracion_segundos // 3600)
        minutos = int((duracion_segundos % 3600) // 60)
        segundos = int(duracion_segundos % 60)

        print(f"\nDistancia: {distancia_km:.2f} km")
        print(f"Duración del viaje: {horas}h {minutos}m {segundos}s")
    else:
        print("Error al obtener los datos:", response.text)

def main():
    while True:
        print("\nIngrese 'q' para salir.")
        origen = input("Ciudad de Origen: ")
        if origen.lower() == 'q':
            break
        destino = input("Ciudad de Destino: ")
        if destino.lower() == 'q':
            break

      
        origen += ",Chile"
        destino += ",Chile"

        obtener_datos_viaje(origen, destino)

if __name__ == "__main__":
    main()
