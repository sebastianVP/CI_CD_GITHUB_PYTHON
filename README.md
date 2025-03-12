c**CAP 1:DEVOPS CONTINUOS INTEGRATION/CONTINUOS DEPLOYMENT**
---
**Overview in 100 seconds:**
DevOps es un conjunto de instrucciones para construir tests y publicar el codigo en una cantidad pequeña de pasos.
DevOps es una integracion continua que permite a los desarrolladores publicar sus codigo en repositorio compartidos.
La figura inicia cuando tenemos desarrolladores: Backend dev y frontend dev que actualizan sus cambios(commit changes)
y los trasladan hacia el repositorio usualmente en github. Cada cambio o commit activa un flujo de trabajo automatico on a *CI Server*
 que permite notificar a los desarrolladores si es que ocurrio algun problema integrando los cambios .
Esto previene lo que se conoce como **MERGE TOWEL**.

Ejemplo:
Tenemos una web app en supongamos node.js, para poner en produccion los cambios de esta app tenemos que ejecutar tres comandos:
- test
- build
- deploy 
Necesariamente tengo que automatizar este proceso usando un servicio de CI como **github actions**:
1. Paso 1:  Lo primero que tenemos que hacer  crear un flujo de trabajo workflow.
2. Paso 2: Decirle que cada que se ejecute run es decir en cada commit o push to the master branch este evento dispara un trabaja que se ejecuta en un contenedor de Linux en la nube.
3. Paso 3: Ejecutar los pasos siguientes, verificar el codigo y el repositorio github, setups nodejs, instalar todas las dependencias y ejecutar los comandos
run, test y deploy.
4. Si alguno de los pasos falla el codigo no sera puesto en produccio ni utilizado por los clientes o consumidores y ademas se informara que hubo un problema durante el despliegue.

Para concluir CI/CD  ofrece dos ventajas:
- Ayuda a automatizar pasos, procesos que de otra forma se tendrian que hacer manualmente.
- Permite detectar los problemas antes de que puedan ir creciendo y generar un desastre y esto resulta en codigo de alta calidad.
```
archivo: .github/workflows/deploy.yml
name: CI/CD is Easy!

on:
   push:
     branches:
      - master

jobs:
   build:
     runs-on:ubuntu-latest
     steps:
     - uses: actions/checkout@v2     get code
     - uses: actions/setups-node@v4      setup node
       with:
           node-version: 12
    -  run: npm ci  # esto significa instalar
    -  run: npm test
    -  run: npm run build              test,build, deploy
    -  run: npm run deploy    
```
