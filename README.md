# Dashboard Home Assistant - energia

Repozytorium zawiera gotowy dashboard Lovelace dla Home Assistanta z widokami
dla:

- paneli fotowoltaicznych,
- banku energii,
- importu i eksportu energii z sieci,
- aktualnego oraz dziennego bilansu domu.

Plik dashboardu: [`home-assistant-energy-dashboard.yaml`](home-assistant-energy-dashboard.yaml).

## Jak uzyc

1. W Home Assistant przejdz do **Ustawienia -> Panele -> Dodaj panel**.
2. Wybierz panel Lovelace w trybie YAML albo otworz edytor surowej konfiguracji
   istniejacego dashboardu.
3. Wklej zawartosc pliku `home-assistant-energy-dashboard.yaml`.
4. Podmien encje `sensor.*` na nazwy encji z Twojej instalacji.
5. Dostosuj zakresy licznikow `max` w kartach `gauge` do mocy instalacji PV,
   falownika i przylacza.

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
| `sensor.grid_power` | Moc sieci: import dodatni, eksport ujemny w W |
| `sensor.grid_voltage` | Napiecie sieci |
| `sensor.grid_import_today` | Import z sieci dzisiaj w kWh |
| `sensor.grid_export_today` | Eksport do sieci dzisiaj w kWh |
| `sensor.grid_import_month` | Import z sieci w tym miesiacu w kWh |
| `sensor.grid_export_month` | Eksport do sieci w tym miesiacu w kWh |

## Uwagi

- Dashboard uzywa tylko standardowych kart Home Assistanta, wiec nie wymaga HACS.
- Dla `sensor.grid_power` przyjeto konwencje: wartosc dodatnia oznacza pobor z
  sieci, wartosc ujemna oznacza oddawanie energii do sieci.
- Jesli Twoj falownik raportuje osobno import i eksport, warto utworzyc sensor
  szablonowy `sensor.grid_power`, ktory laczy te wartosci w jeden bilans.
