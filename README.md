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

    - Opis szczegółowy, dla użytkownika

    ```txt
    System sygnalizacji świetlnej będzie zarządzał
    ruchem na skrzyżowaniu drogi głównej z drogą
    podporządkowaną. Po drogach tym poruszają
    się samochody oraz piesi, a na głównej
    drodze również tramwaje.

    Ruch samochodów jest zarządzany standardowo.

    Jeżeli przez główną drogę i torowisko chce przejść
    pieszy, to naciska przycisk i po pewnym czasie dostaje
    zielone światło. Analogicznie wygląda sytuacja pieszych
    poruszających się równolegle do drogi głównej.

    Dla tramwajów znajdują się zamontowane w torowisku
    czujniki, które po wykryciu tramwaju zmieniają jego
    sygnał na "Jedź". Dają mu więc priorytet.

    Jeżeli do skrzyżowania zbliżać się będzie pojazd
    uprzywilejowany, to na jego kierunku zostanie
    ustawione zielone światło, aby prościej mu
    było pokonać to skrzyżowanie. Stanie się
    to poprzez nadanie przez pojazd
    sygnału radiowego, który zostanie odebrany
    przez odpowiedni odbiornik na skrzyżowaniu.
    ```
    

4. **Komponenty**:
    - system `UrbanTrafficSystem` - system nadrzędny, pomagający spiąć ze sobą system świateł oraz pojazdów uprzywilejowanych,
    - system `TrafficLightsSystem` - system sygnalizacji świetlnej,
    - system `EmergencyVehicleSystem` - system nadający sygnały w pojeździe uprzywilejowanym,
    - device `CarTrafficLight` - sygnalizator świetlny dla samochodów,
    - device `TramTrafficLight` - sygnalizator świetlny dla tramwajów,
    - device `PedTrafficLight` - sygnalizator świetlny dla pieszych,
    - device `PedButton` - przycisk dla pieszych, którego naciśnięcie powiadamia kontroler o tym, że pieszy oczekuje na sygnał zielony,
    - device `TramSensor` - czujnik wykrywający zbliżający się tramwaj, działa podobnie do przycisku dla pieszych,
    - device `RadioReceiver` - odbiornik sygnału wysyłanego przez pojazdy uprzywilejowane,
    - device `RadioSignalEmitter` - nadajnik sygnału radiowego w pojeździe uprzywilejowanym,
    - device `EmiteSignalButton` - przycisk pozwalający nadać sygnał z pojazdu uprzywilejowanego,
    - processor `CPU` - procesor działający w układzie sterującym sygnalizacją świetlną,
    - processor `VehicleCPU` - procesor zamontowany w pojeździe uprzywilejowanym,
    - memory `Mem`, `VehicleMem` - pamięć, odpowiednio dla sygnalizacji i dla pojazdu,
    - bus `CommBus`, `VehicleBus` - magistrale, odpowiednio dla sygnalizacji i dla pojazdu,
    - bus `Radio` - fale radiowe spinające służące do komunikacji pojazdu uprzywilejowanego,
    - process `MainController` - proces sterujący działaniem sygnalizacji świetlnej, to on przyjmuje requesty i rozsyła sygnały do każdego sygnalizatora,
    - process `EmergencyVehicleController` - proces, który pośredniczy pomiędzy przyciskiem w pojeździe uprzywilejowanym, a nadajnikiem,
    - thread `PedButtonThread`, `TramSensorThread` - wątki dla przycisku i sensorów, pośredniczą w wysyłaniu próśb o zielone światło,
    - thread `LightThread` - wątek pośredniczący w komunikacji między kontrolerem a sygnalizatorem, odbiera od kontrolera sygnał i wysyła mu status sygnalizatora,
    - thread `RadioReceiverThread` - wątek odpowiadający za odbieranie żądań od pojazdów uprzywilejowanych
