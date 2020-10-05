# Stuttgart Open Motorway Project (STOMP) - A SUMO Traffic Scenario

A synthetic 24 hour traffic scenario for a 45 km section of the German highway A81 between Stuttgart Feuerbach - Heilbronn (Baden-Württemberg) based on realistic traffic data. The traffic scenario was used in the following publication (please add a citation when using it):

*David Förster, Hans Löhr, Anne Grätz, Jonathan Petit, and Frank Kargl, "**An Evaluation of Pseudonym Changes for Vehicular Networks in Large-scale, Realistic Traffic Scenarios**", IEEE Transactions on Intelligent Transportation Systems 19.10 (2017): 3400-3405, doi: [10.1109/TITS.2017.2775519](https://doi.org/10.1109/TITS.2017.2775519).*

The scenario map is based on http://wwww.openstreetmap.org. It contains 24 hours of traffic created based on publicly available data from German traffic authorities ([Federal Highway Research Institute BaST](http://www.bast.de/DE/Verkehrstechnik/Fachthemen/v2-verkehrszaehlung/Stundenwerte.html) and  [Road Traffic Center Baden-Württemberg](https://www.svz-bw.de/verkehrszaehlung/automatische-strassenverkehrszaehlung), both from 2013). Four different vehicle classes are included in the scenario (passenger cars, motor bikes, trucks, and buses) with realistic acceleration profiles. There are two flavors of the scenario: One based on work day traffic data (incl. Saturday) and one for Sunday traffic data.

While the number of passing vehicles before and after every highway exit are based on real traffic data, we had no information about how many vehicles exit and enter the highway on each exit. Therefore, we applied a best-guess estimation.

The scenario is provided as-is. It is not actively maintained and will not be adapted to work with newer SUMO versions. We welcome forks of the project (according to the license) provided that a reference to the original publication is added. If you have any questions, please reach out to David Förster (david.foerster@de.bosch.com).

## How to run the simulation

The scenario is compatible with SUMO (https://sumo.dlr.de) version 0.25.

### Create trips

Create routes from the flow definitions using the `duarouter`tool bundled with SUMO.

```shell
# For working days ...
duarouter -c flowstoroutes_workday.cfg.xml
# ... and for Sundays
duarouter -c flowstoroutes_sunday.cfg.xml
```

### Run the simulation

SUMO parameters in the configuration files are as used in the simulations for our publication.

```shell
# For working days ...
sumo -c Simulation_workday.sumo.cfg.xml
# ... and for Sundays.
sumo -c Simulation_sunday.sumo.cfg.xml
```

Please be aware that at the beginning of the simulation, the scenario is completely empty. Therefore, you will have to wait until the highway is fully populated with vehicles before starting any analysis. For our publication, we used a low traffic scenario (1 to 4 am) and a high traffic scenario (7 to 10 am), running the simulation for the full 24 hours and cropping the output respectively.

The SUMO FCD output will be several Gigabytes. Using a named pipe to run the output through gzip can help reduce file size.

## Licenses

The SUMO network *simulation/Highway.net.xml* (which is based on openstreetmap.org input) is made available under the Open Database License: http://opendatacommons.org/licenses/odbl/1.0/. Any rights in individual contents of the database (in the form of the SUMO network) are licensed under the Database Contents License: http://opendatacommons.org/licenses/dbcl/1.0/.

All other files (traffic data and configuration) are licensed under a Creative Commons Attribution-ShareAlike 4.0 International License: http://creativecommons.org/licenses/by-sa/4.0/.
