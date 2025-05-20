# Systemy czasu rzeczywistego - projekt

1. **Tytuł modelu**:
    - Skrzyżowanie z sygnalizacją świetlną

2. **Dane studenta**:
    - Piotr Klęp
    - <pklep@student.agh.edu.pl>

3. **Opis modelowanego systemu**:
    - Opis ogólny

    ```txt
    Zamodelowany system jest systemem sygnalizacji świetlnej
    na skrzyżowaniu z ruchem samochodowym, tramwajowym i pieszym.
    Poza samymi sygnalizatorami system ten zawiera przyciski
    dla pieszych oraz czujniki wykrywające zbliżające się tramwaje.
    ```

    - Opis szczegółowy

    ```txt
    System będzie kontrolował ruch na skrzyżowaniu z
    czterema wlotami dla samochodów, ruchem pieszym
    oraz ruchem tramwajowym poprowadzonym równolegle
    między jezdniami na jednym kierunku.

    Jezdnia z torowiskiem będzie drogą tzw. główną.
    Pozostałe 2 wloty będą wlotami dróg niższej kategorii
    (a więc o mniejszym ruchu).

    Jeżeli nie będzie pieszych oraz tramwajów, to
    czas sygnału zielonego na głównej drodze
    będzie zależał tylko od tego, czy na
    drogach podporządkowanych będą czekały jakieś
    inne pojazdy (stąd 'VehicleSensor'), bądź od
    pojawienia się pojazdu uprzywilejowanego.
    Brak pojazdów na drogach podporządkowanych, to
    ciągły zielony sygnał dla głównej drogi.

    Jeżeli przez główną drogę i torowisko chce przejść
    pieszy, to naciska przycisk i po pewnym czasie dostaje
    zielone światło. Równocześnie zielony sygnał otrzymują
    pojazdy na drogach podporządkowanych, równoległych
    do tego przejścia dla pieszych.
    Analogicznie wygląda sytuacja pieszych poruszających
    się równolegle do drogi głównej.

    Dla tramwajów znajdują się zamontowane w torowisku
    czujniki, które po wykryciu tramwaju zmieniają jego
    sygnał na tzw. pionową szczelinę (|), a sygnały
    dla pieszych i pojazdów z drogi podporządkowanej
    - na sygnał czerwony. Równolegle do tramwaju mogą
    się poruszać samochody na głównej drodze.

    Jeżeli do skrzyżowania zbliżać się będzie pojazd
    uprzywilejowany, to na jego kierunku zostanie
    ustawione zielone światło, aby prościej mu
    było pokonać to skrzyżowanie. Pojazdy
    uprzywilejowane mają tutaj największy priorytet.
    ```
    

4. **Komponenty**:
    - `system TrafficLightSystem` - główny system sterujący pracą sygnalizacji świetlnej
    - `device VehicleSignal` - sygnalizator świetlny dla zwykłych pojazdów (3 kolory)
    - `device PedestrianSignal` - sygnalizator świetlny dla pieszych (2 kolory)
    - `device TramSignal` - sygnalizator świetlny dla tramwajów (2 sygnały)
    - `device VehicleSensor` - czujnik zwykłych pojazdów
    - `device PedestrianButton` - przycisk wzbudzający sygnalizację dla pieszych
    - `device TramSensor` - czujnik dający priorytet tramwajom
    - `thread Timer` - wątek odliczający pozostały czas do zmiany sygnału świetlnego na skrzyżowaniu (chyba, że zostanie nadpisany przez priorytet)
    - `thread EmergencyVehiclePriority` - wątek nadpisujący timer, daje on priorytet pojazdom uprzywilejowanym
    - `bus CommunicationBus` - magistrala służąca do komunikowania się komponentów
