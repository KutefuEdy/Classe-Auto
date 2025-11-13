# Classe-Auto
class Auto:
    def __init__(self, targa, marca, modello):
        self.targa = targa
        self.marca = marca
        self.modello = modello

    def stampa(self):
        print("targa:", self.targa, "marca:", self.marca, "modello:", self.modello)


class PostoAuto:
    def __init__(self, numero):
        self.numero = numero
        self.auto = None

    def occupa(self, auto):
        if self.auto == None:
            self.auto = auto
            print("il posto", self.numero, "ora è occupato da", auto.targa)
        else:
            print("il posto", self.numero, "è già occupato")

    def libera(self):
        if self.auto != None:
            print("il posto", self.numero, "è stato liberato")
            self.auto = None
        else:
            print("il posto", self.numero, "è già libero")

    def stato(self):
        if self.auto == None:
            return "posto " + str(self.numero) + ": libero"
        else:
            return "posto " + str(self.numero) + ": occupato da " + self.auto.targa


class Parcheggio:
    def __init__(self, nome):
        self.nome = nome
        self.posti = []

    def aggiungi_posto(self, posto):
        self.posti.append(posto)

    def mostra_posti(self):
        print("stato del parcheggio", self.nome + ":")
        for posto in self.posti:
            print(posto.stato())

    def parcheggia(self, auto):
        for posto in self.posti:
            if posto.auto == None:
                posto.occupa(auto)
                return
        print("non ci sono posti liberi disponibili")

    def rimuovi_auto(self, targa):
        for posto in self.posti:
            if posto.auto != None and posto.auto.targa == targa:
                posto.libera()
                return
        print("nessuna auto con targa", targa, "trovata nel parcheggio")

    def cerca_auto(self, targa):
        for posto in self.posti:
            if posto.auto != None and posto.auto.targa == targa:
                print("l'auto con targa", targa, "si trova nel posto numero", posto.numero)
                return
        print("l'auto con targa", targa, "non è presente nel parcheggio")


p = Parcheggio("parcheggio centrale")

for i in range(1, 6):
    p.aggiungi_posto(PostoAuto(i))

a1 = Auto("AB123CD", "Fiat", "Panda")
a2 = Auto("EF456GH", "Tesla", "Model 3")

p.parcheggia(a1)
p.parcheggia(a2)

p.mostra_posti()

p.cerca_auto("AB123CD")

p.rimuovi_auto("AB123CD")

p.mostra_posti()