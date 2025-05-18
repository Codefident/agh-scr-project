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
