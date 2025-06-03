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

    Przykładowe skrzyżowanie (_źródło: Google Maps_)
   ![Screenshot from 2025-06-03 13-23-06](https://github.com/user-attachments/assets/694396a5-5f10-4772-baef-3c02791ab7a6)

    Przykładowy pojazd uprzywilejowany (_źródło: Wikisłownik)
    ![image](https://github.com/user-attachments/assets/e160ba80-7e08-42d2-8d24-1629c221fb5e)


    

5. **Komponenty**:
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
  
6. **Model - schematy**
   - `UrbanTrafficSystem`
     ![Screenshot from 2025-06-03 03-13-24](https://github.com/user-attachments/assets/e218a097-983d-4473-b1a2-224142532c33)

   - `TrafficLightsSystem`
    ![Screenshot from 2025-06-03 03-12-48](https://github.com/user-attachments/assets/60668034-4020-4ba6-98f1-78b692676938)

     
   - `EmergencyVehicleSystem`
   ![Screenshot from 2025-06-03 03-10-04](https://github.com/user-attachments/assets/bda19caa-292e-4558-ba7f-70a90d7d9095)

7. **Analizy modelu**
   - Check Binding Constraints - "No problems found" ✅
   - Check Connection Binding Consistency - Brak ostrzeżeń oraz błędów ✅
  
8. **Inne informacje zależne od tematu**
    Brak.

9. **Literatura**
   - [https://en.wikipedia.org/wiki/Traffic_signal_preemption#Vehicular_device_types](https://en.wikipedia.org/wiki/Traffic_signal_preemption#Vehicular_device_types)
   - [https://leotek.com/traffic-light-sensors/](https://leotek.com/traffic-light-sensors/)
