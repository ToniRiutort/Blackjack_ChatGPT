# Blackjack_ChatGPT
Juego de mesa del blackjack creado con la IA llamada ChatGPT
CÓDIGO EN PYTHON DEL JUEGO 
def valor_carta(carta):
    if carta in ["J", "Q", "K"]:
        return 10
    elif carta == "A":
        return 11
    else:
        return int(carta)

def jugar_ronda(baraja):
    mano_jugador = []
    mano_dealer = []
    puntos_jugador = 0
    puntos_dealer = 0
    for i in range(2):
        carta = baraja.pop(0)
        mano_jugador.append(carta)
        puntos_jugador += valor_carta(carta)
        carta = baraja.pop(0)
        mano_dealer.append(carta)
        puntos_dealer += valor_carta(carta)
    print("Tus cartas son: " + str(mano_jugador) + " (total de " + str(puntos_jugador) + " puntos)")
    print("La carta del dealer es: " + str(mano_dealer[0]))
    if puntos_jugador == 21:
        print("¡Blackjack! Ganas.")
        return
    while puntos_jugador < 21:
        accion = input("¿Quieres seguir tomando cartas? (s/n) ")
        while accion != "s" and accion != "n":
            accion = input("Respuesta inválida, elige de nuevo: ")
        if accion == "n":
            break
        carta = baraja.pop(0)
        mano_jugador.append(carta)
        puntos_jugador += valor_carta(carta)
        print("Tus cartas ahora son: " + str(mano_jugador) + " (total de " + str(puntos_jugador) + " puntos)")
        if puntos_jugador > 21:
            print("Te pasaste de 21. Pierdes.")
            return
    while puntos_dealer < 17:
        carta = baraja.pop(0)
        mano_dealer.append(carta)
        puntos_dealer += valor_carta(carta)
    print("La mano final del dealer es: " + str(mano_dealer) + " (total de " + str(puntos_dealer) + " puntos)")
    if puntos_dealer > 21:
        print("El dealer se pasó de 21. Ganas.")
    elif puntos_dealer > puntos_jugador:
        print("El dealer gana. Pierdes.")
    elif puntos_dealer == puntos_jugador:
        print("Empate.")
    else:
        print("Ganas!")

def jugar_juego():
    baraja = [2, 3, 4, 5, 6, 7, 8, 9, 10, "J", "Q", "K", "A"] * 4
    nombre = input("Ingresa tu nombre: ")
    print("Bienvenido a Blackjack, " + nombre + "!")
    while True:
        jugar_ronda(baraja)
        seguir_jugando = input("Quieres jugar otra ronda? (s/n) ")
        while seguir_jugando != "s" and seguir_jugando != "n":
            seguir_jugando = input("Respuesta inválida, elige de nuevo: ")
        if seguir_jugando == "n":
            print("Gracias por jugar Blackjack, " + nombre + "!")
            break
jugar_juego()
