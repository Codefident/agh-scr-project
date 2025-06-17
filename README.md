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

    Przykładowe skrzyżowanie (_źródło: Google Maps_)<br/>
   ![Screenshot from 2025-06-03 13-23-06](https://github.com/user-attachments/assets/694396a5-5f10-4772-baef-3c02791ab7a6)

    Przykładowy pojazd uprzywilejowany (_źródło: Wikisłownik_)<br/>
    ![image](https://github.com/user-attachments/assets/e160ba80-7e08-42d2-8d24-1629c221fb5e)

5. **Komponenty**:
    - **data**:
        - data `Signal` - enumerator, wartości `"Go", "Stop", "ChangingSignal", "Failure"`, odpowiada za to jaki powinien być emitowany sygnał,
        - data `RequestSignal` - boolean, odpowiada za żądanie zmiany świateł przez np. pieszego,
        - data `LightStatus` - boolean, odpowiada za status świateł drogowych (czy działają, czy nie),
        - data `EmergencySignal` - string, odpowiada za sygnał wysyłany przez pojazdy uprzywilejowane,
    - **system**:
        - system `UrbanTrafficSystem` - system nadrzędny, pomagający spiąć ze sobą system świateł oraz pojazdów uprzywilejowanych,
        - system `TrafficLightsSystem` - system sygnalizacji świetlnej,
        - system `EmergencyVehicleSystem` - system nadający sygnały w pojeździe uprzywilejowanym,
    - **device**:
        - device `CarTrafficLight` - sygnalizator świetlny dla samochodów,
        - device `TramTrafficLight` - sygnalizator świetlny dla tramwajów,
        - device `PedTrafficLight` - sygnalizator świetlny dla pieszych,
        - device `PedButton` - przycisk dla pieszych, którego naciśnięcie powiadamia kontroler o tym, że pieszy oczekuje na sygnał zielony,
        - device `TramSensor` - czujnik wykrywający zbliżający się tramwaj, działa podobnie do przycisku dla pieszych,
        - device `RadioReceiver` - odbiornik sygnału wysyłanego przez pojazdy uprzywilejowane,
        - device `RadioSignalEmitter` - nadajnik sygnału radiowego w pojeździe uprzywilejowanym,
        - device `EmiteSignalButton` - przycisk pozwalający nadać sygnał z pojazdu uprzywilejowanego,
    - **processor**:
        - processor `CPU` - procesor działający w układzie sterującym sygnalizacją świetlną,
        - processor `VehicleCPU` - procesor zamontowany w pojeździe uprzywilejowanym,
    - **memory**:
        - memory `Mem`, `VehicleMem` - pamięć, odpowiednio dla sygnalizacji i dla pojazdu,
    - **bus**:
        - bus `CommBus`, `VehicleBus` - magistrale, odpowiednio dla sygnalizacji i dla pojazdu,
        - bus `Radio` - fale radiowe spinające służące do komunikacji pojazdu uprzywilejowanego,
    - **process**:
        - process `MainController` - proces sterujący działaniem sygnalizacji świetlnej, to on przyjmuje requesty i rozsyła sygnały do każdego sygnalizatora,
        - process `EmergencyVehicleController` - proces, który pośredniczy pomiędzy przyciskiem w pojeździe uprzywilejowanym, a nadajnikiem,
    - **thread**:
        - thread `PedButtonThread`, `TramSensorThread` - wątki dla przycisku i sensorów, pośredniczą w wysyłaniu próśb o zielone światło,
        - thread `LightThread` - wątek pośredniczący w komunikacji między kontrolerem a sygnalizatorem, odbiera od kontrolera sygnał i wysyła mu status sygnalizatora,
        - thread `RadioReceiverThread` - wątek odpowiadający za odbieranie żądań od pojazdów uprzywilejowanych
  
7. **Model - schematy** - diagramy systemów, dla czytelności pierwsze 3 bez wyświetlonych `actual bindings`, kolejne 2 już je zawierają:
   - `UrbanTrafficSystem`<br/>
     ![urbanTrafficDiagram](https://github.com/Codefident/agh-scr-project/blob/main/diagrams-images/urbanTrafficDiagram.svg)

   - `TrafficLightsSystem`<br/>
    ![trafficLightsDiagram](https://github.com/Codefident/agh-scr-project/blob/main/diagrams-images/trafficLightsDiagram.svg)
     
   - `EmergencyVehicleSystem`<br/>
   ![emergencyVehicleDiagram](https://github.com/Codefident/agh-scr-project/blob/main/diagrams-images/emergencyVehicleDiagram.svg)

    **Schematy z bindingami**

    - `trafficLightsDiagram` z actual bindings<br/>
    ![trafficLightsDiagramBindings](https://github.com/Codefident/agh-scr-project/blob/main/diagrams-images/trafficLightsDiagramBindings.png)

    - `EmergencyVehicleSystem` z actual bindings<br/>
    ![emergencyVehicleDiagram](https://github.com/Codefident/agh-scr-project/blob/main/diagrams-images/emergencyVehicleDiagramBindings.png)

8. **Analizy modelu**
   - Check Binding Constraints - "No problems found" ✅<br/>
     ![image](https://github.com/user-attachments/assets/0e54d590-d4a0-4e58-a400-5cf813cb57d0)

   - Check Connection Binding Consistency - Brak ostrzeżeń oraz błędów ✅<br/>
     ![image](https://github.com/user-attachments/assets/004e7c23-1ea1-47af-a44e-c470a21b75ab)

   - Weight Totals, gdzie maksymalna łączna waga ustawiona została na 300kg i nie została przekroczona ✅:<br/>
     ![image](https://github.com/user-attachments/assets/c21a1c7a-dba8-4fa6-a6f4-a260d9f744a6)

  
9. **Inne informacje zależne od tematu**
    Brak.

10. **Literatura**
   - [https://en.wikipedia.org/wiki/Traffic_signal_preemption#Vehicular_device_types](https://en.wikipedia.org/wiki/Traffic_signal_preemption#Vehicular_device_types)
   - [https://leotek.com/traffic-light-sensors/](https://leotek.com/traffic-light-sensors/)
