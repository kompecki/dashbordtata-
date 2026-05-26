# Dashboard Home Assistant - energia

Repozytorium zawiera dwa dashboardy Lovelace dla Home Assistanta:

- `home-assistant-energy-dashboard.yaml` - prosty dashboard na standardowych kartach Home Assistanta.
- `home-assistant-energy-flow-wow.yaml` - efektowny dashboard w stylu energy flow z animacjami, ciemnym motywem, centralnym inwerterem, bankiem energii, siecia i wykresami.

## Polecana wersja: Energy Flow Pro

Plik: [`home-assistant-energy-flow-wow.yaml`](home-assistant-energy-flow-wow.yaml)

To jest bardziej wizualna wersja inspirowana ekranami typu falownik / magazyn energii:

- animowane linie przeplywu energii,
- centralny inwerter,
- orbitujace slonce z produkcja PV,
- bank energii z animowanym wypelnieniem,
- siec z trybem import / eksport,
- dom i opcjonalna ladowarka EV,
- szklane kafle parametrow,
- wykresy mocy i historii energii.

### Wymagane dodatki HACS

Wersja `Energy Flow Pro` uzywa custom kart:

1. `button-card`
2. `apexcharts-card`

Po instalacji przez HACS upewnij sie, ze zasoby Lovelace sa dodane:

```yaml
resources:
  - url: /hacsfiles/button-card/button-card.js
    type: module
  - url: /hacsfiles/apexcharts-card/apexcharts-card.js
    type: module
```

Jesli nie chcesz uzywac HACS, uzyj prostszego pliku `home-assistant-energy-dashboard.yaml`.

## Jak uzyc

1. W Home Assistant przejdz do **Ustawienia -> Panele -> Dodaj panel**.
2. Wybierz panel Lovelace w trybie YAML albo otworz edytor surowej konfiguracji istniejacego dashboardu.
3. Wklej zawartosc wybranego pliku YAML.
4. Podmien encje `sensor.*` na nazwy encji z Twojej instalacji.
5. Dostosuj zakresy, jednostki i nazwy sensorow do falownika, magazynu energii i licznika.

## Encje do podmiany

Dashboard zaklada nastepujace encje. Nazwy sa przykladowe:

| Encja | Znaczenie |
| --- | --- |
| `sensor.pv_power` | Aktualna moc produkcji paneli PV w W |
| `sensor.pv_energy_today` | Energia wyprodukowana dzisiaj w kWh |
| `sensor.pv_energy_month` | Energia wyprodukowana w tym miesiacu w kWh |
| `sensor.house_power` | Aktualne zuzycie domu w W |
| `sensor.house_energy_today` | Dzienne zuzycie domu w kWh |
| `sensor.energy_bank_state_of_charge` | Poziom naladowania banku energii w % |
| `sensor.energy_bank_power` | Moc netto banku energii w W |
| `sensor.energy_bank_charge_power` | Moc ladowania banku energii w W |
| `sensor.energy_bank_discharge_power` | Moc rozladowania banku energii w W |
| `sensor.energy_bank_energy_charged_today` | Energia naladowana do banku dzisiaj w kWh |
| `sensor.energy_bank_energy_discharged_today` | Energia oddana z banku dzisiaj w kWh |
| `sensor.energy_bank_temperature` | Temperatura banku energii |
| `sensor.energy_bank_status` | Tryb pracy banku lub falownika |
| `sensor.inverter_temperature` | Temperatura inwertera, opcjonalna dla wersji Flow Pro |
| `sensor.grid_power` | Moc sieci: import dodatni, eksport ujemny w W |
| `sensor.grid_voltage` | Napiecie sieci |
| `sensor.grid_import_today` | Import z sieci dzisiaj w kWh |
| `sensor.grid_export_today` | Eksport do sieci dzisiaj w kWh |
| `sensor.grid_import_month` | Import z sieci w tym miesiacu w kWh |
| `sensor.grid_export_month` | Eksport do sieci w tym miesiacu w kWh |
| `sensor.ev_charger_power` | Moc ladowarki EV, opcjonalna |

## Konwencje

- `sensor.grid_power` dodatni oznacza pobor z sieci, ujemny oznacza eksport do sieci.
- `sensor.energy_bank_power` dodatni oznacza ladowanie banku, ujemny oznacza oddawanie energii.
- Sensory mocy sa zakladane w W, a dashboard pokazuje je jako kW.
- Sensory energii dziennej sa zakladane w kWh.

## Gdy cos sie nie wyswietla

- Sprawdz, czy custom karty z HACS sa zainstalowane i dodane jako zasoby.
- Sprawdz, czy encje istnieja w **Narzedzia deweloperskie -> Stany**.
- Jesli Home Assistant pokazuje blad typu `Custom element does not exist`, brakuje zasobu HACS.
- Jesli widzisz `unknown` albo `unavailable`, trzeba podmienic nazwe encji na prawidlowa.
