# Configuración proyecto Angular y Pipeline

## Tabla de contenido
- [Configuración de Angular](#Configuracion-de-Angular).
- [Configuración del package.json](#Configuración-del-package.json).
- [Configuración del karma.conf.js](#Configuración-del-karma.conf.js).
- [Nota](#Nota).
- [Pipeline](#Pipeline).
- [Reporte en Sonar](#Reporte-en-Sonar).

## Documentaciones

- **Documentación testSuite y reporte en testexecutions:** [testSuite](https://community.sonarsource.com/t/need-help-on-error-expected-testexecutions-but-got-testsuite-at-line-2-i-am-trying-to-show-unit-test-count-on-sonar-dashboard-for-scala-and-angular-node-mocha-and-jasmine-framework-used-istambul-reporter-is-used/45150/3)

### Configuración de Angular

La pre-configuración que se realizó en el proyecto angular fue:

#### Configuración del package.json

[![1.png](https://i.postimg.cc/Rh5VRJSF/1.png)](https://postimg.cc/tZkjRTVQ)

El devDependecies, contiene karma, que es el test-runner y jasmine que es la suite de test.

Dependecias importantes:

`    "karma": "^1.7.1",
    "karma-chrome-launcher": "~2.2.0",
    "karma-coverage": "^2.1.0",
    "karma-coverage-istanbul-reporter": "^2.0.6",
    "karma-jasmine": "~1.1.1",
    "karma-jasmine-html-reporter": "^0.2.2",
    "karma-junit-reporter": "^1.0.4",
    "karma-phantomjs-launcher": "^1.0.4"`

#### Configuración del karma.conf.js

[![2.png](https://i.postimg.cc/kMsNXLCB/2.png)](https://postimg.cc/rzdRfnKk)

El archivo karma.conf.js contine la configuración de las pruebas unitarias, es importante  tener en cuenta que cualquier dependecia que este en el **package.json** y que sea necesario para las pruebas unitarias debe ir en plugins(**sombreado en la imagen de color naranja**)


- **coverageIstanbulReporter(cuadro naranja en la imagen)**: contiene la ruta relativa donde creara la carpera "coverage" y los formatos de reporte, los cuales para este proyecto son, **html, lcovonly, text-summary**. Para el reporte efectivo en sonarQube, se debe poner **lcovonly**, en formato de reporte, puesto que posteriormente se utilizara una propiedad para extraer la cobertura.
 
- **reporters(cuadro azul en la imagen)**: en reporters se debe especificar en que va a reportar el proyecto, para este proyecto fue **progress**, **kjhtml**, **junit**, además se configura los navegadores en los cuales se realizaran las pruebas; en el caso de este proyecto fueron **ChromeHeadless**, **PhantomJS**.

- **JunitReporter(Cuadro de color morado)**: tiene la creación de la carpeta que contendrá los archivos y el nombre del archivo que en este caso es  **Test.xml**

#### Nota
Al generar el archivo xml del número de test, el reporte tiene la etiqueta testsuite y sonar admite testExecutions, por este formato que genera jasmine, no se puede reportar el número de pruebas unitarias en el proyecto.

### Pipeline

nombre del pipeline: Angular-CI-install-PrepareSonar-Build-Test-Publish [Angular-CI-install-PrepareSonar-Build-Test-Publish](https://dev.azure.com/celuladevops/Celula/_build?definitionId=54)

El pipeline diseñado es:
[![3.jpg](https://i.postimg.cc/L84c5QCN/3.jpg)](https://postimg.cc/9rS8Nbj7)

### Reporte en Sonar

[![screencapture-sonarjason22-eastus-cloudapp-azure-9000-dashboard-2021-12-10-17-34-15.png](https://i.postimg.cc/Vv7rXVwm/screencapture-sonarjason22-eastus-cloudapp-azure-9000-dashboard-2021-12-10-17-34-15.png)](https://postimg.cc/wRmjpF3G)


# TestApp

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 6.1.3.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.


## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).
