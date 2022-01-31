# [Curso de Next.js: Optimización y Deploy a Producción](https://platzi.com/clases/nextjs-deploy/)

## Este curso es la continuacion del curso de Next.js: Sitios Estáticos y Jamstack. [Repo](https://github.com/BraianVayletGlobant/curso-next-sitios-estaticos-jamstack-platzi)

#### CMS usado en el proyecto: [Contentfull](https://app.contentful.com/)

## Clases

- Clase1: Presentacion
- Clase2: [¿Para qué necesitamos variables de entorno?](#¿Para-qué-necesitamos-variables-de-entorno?)
- Clase3: [Moviendo las llaves a variables de entorno](#Moviendo-las-llaves-a-variables-de-entorno)
- Clase4: [Llaves de alcance público (browser) y privadas (server)](<#Llaves-de-alcance-público-(browser)-y-privadas-(server)>)
- Clase5: [Paquete cross-env y consideraciones en otros sistemas operativos](#Paquete-cross-env-y-consideraciones-en-otros-sistemas-operativos)
- Clase6: [Componente Image de Next.js](#Componente-Image-de-Next.js)
- Clase7: [Image API: configurando nuestro propio loader avanzado](#Image-API:-configurando-nuestro-propio-loader-avanzado)

---

# ¿Para qué necesitamos variables de entorno?

## 🧩 Variables de entorno

### Ideas/conceptos claves

Una variable de entorno es una variable dinámica que puede afectar al comportamiento de los procesos en ejecución en un ordenador. Son parte del entorno en el que se ejecuta un proceso.

### Apuntes

- Generalmente, son secretos que solo una máquina en particular debe saber. Ej.: la contraseña de la base de datos
  - Permite almacenar una “contraseña” donde únicamente nos interesa
- No deben versionarse
  - Peor aún si el repositorio es público, ya que existe montones de bots automatizados para encontrar estas llaves

```cmd
   💡 En caso de subir por accidente una variable de entorno, no sirve de nada crear otro commit, porque quedará en la historia del repositorio, la mejor solución es crear otra llave de entorno
```

### ¿Qué buscamos?

1. Los secretos no sean compartidos, pero…
2. Como desarrollador quiero conocer que secretos necesito para que la aplicación funcione.

   - Debe ser una lista clara la cual especifique que llaves necesito para que la aplicación no tenga ningún problema

3. La aplicación debe ser capaz de cargar y leer nuestros secretos

### Implementación

- Existen diferentes formas de implementar las variables de entorno, una de ellas es la siguiente estructura, donde existe:
- Documento de ejemplo

### Versionado

- Contiene una lista de llaves necesarias
- Sin los valores de las llaves ⇒ En el peor de los casos puede existir algún valor, pero es porque nada malo pueda pasar

```
ACCESS_TOKEN=
URL_DB=
```

### Una copia del documento

- Ignorado por el versionador (Git).
- Contiene las llaves necesarias con valores necesarios.

## 📌 **RESUMEN:**

Las variables de entorno, son la mejor forma de poder guardar contraseñas, llaves, etc. (secretos) ya que estas no son compartidas, establece una lista clara de que secretos necesita la aplicación para que no se rompa y es capaz de cargar y leer dichos valores de la lista de secretos

> Links:
>
> - [variables de entorno en node](https://www.youtube.com/watch?v=tZ3bLXoD6i0)

# Moviendo las llaves a variables de entorno

## 🖱 Variables de entorno en Next.js

### Apuntes

- Existen dos tipos de variables de entorno en Next.js, estas se diferencian principalmente del lugar de ejecución ya sea en el navegador o en el servidor
- La forma en la que maneja Next.js las llaves es de la siguiente forma:
  - MY_VARIABLE: Solo disponible en el servidor (Node.js)
  - NEXT_PUBLIC_MY_VARIABLE: Disponible en el cliente (navegador)
- El motivo por el que Next.js requiere agregar el prefijo NEXT_PUBLIC es porque de esta manera te hace consiente que esta variable estará expuesta públicamente en el navegador

## 📌 **RESUMEN:**

Next.js administra las variables según las necesitemos en el servidor o lleguen al cliente, estas últimas implican que podrán estar expuestas en el navegador. Para hacerte consiente de la implementación de la misma requiere el prefijo `NEXT_PUBLIC`

> Links:
>
> - [Environment Variables](https://nextjs.org/docs/basic-features/environment-variables)
> - [Environment Variables - config](https://nextjs.org/docs/api-reference/next.config.js/environment-variables)

# Llaves de alcance público (browser) y privadas (server)

Variables de entorno en NextJs.

Si las nombramos como NEXT_PUBLIC_MY_VARIABLE estas van a poder ser accesibles desde el clinete como desde el servidor, gracias a agregar el NEXT_PUBLIC

En el caso de que las nombremos como MY_VARIABLE, seran solo accesibles desde el servidor de Node.js y desde el fichero api.

# Paquete cross-env y consideraciones en otros sistemas operativos

**cross-env:** es una utilidad que sirve para que las variables de entorno sean reconocidas y se puedan utilizar independientemente del sistema operativo en el que estemos desarrollando.

La gran mayoría de los servicios de internet y de servidores ya cuentan con soporte para incorporar variables de entorno, tal es el caso de:

- Vercel
- Heroku
- Github Actions, entre otras

Si bien las variables de entorno existen hace mucho tiempo, no significa que funcionen de la misma forma en todos los sistemas
operativos

_“La forma de cargar variables de entorno puede variar por sistema operativo”_

Principalmente en Windows y Linux existe una gran diferencia. Ej:

```bash
# Windows
set MY_SECRET=<your token here>

# Unix (macOS + Linux)
export MY_SECRET=<your token here>
```

### La solución es utilizar siempre **cross-env**

Es una buena práctica, Next.js ya cuenta integrado por si mismo este paquete, pero para otro tipo de proyectos o aplicaciones, es muy buena práctica utilizarlo.

Además, que la mayoría de los servidores ya cuenta con soporte para las variables de entorno

> Links:
>
> - [Encrypted secrets - GitHub Docs](https://docs.github.com/es/actions/security-guides/encrypted-secrets)
> - [Configuration and Config Vars](https://devcenter.heroku.com/articles/config-vars)
> - [Environment Variables](https://vercel.com/docs/concepts/projects/environment-variables)

# Componente Image de Next.js

### ¿Cómo funciona?

Next.js va creando imágenes de diferentes tamaños en el servidor, las cuales según el tamaño del dispositivo se irán cargando.

Existen servidores los cuales se encargan únicamente de la manipulación de imágenes, los cuales están optimizados para el manejo de imágenes a gran escala y Next.js brinda la flexibilidad para el uso de los mismos

Entonces, para la imágenes que están guardadas de manera local es decir dentro de la carpeta del proyecto es necesario hacer un import de la ruta de la imagen por ejemplo:

```js
import profilePic from '../public/picture.png'
```

Next.js va a determinar el width y el height de la imagen.
Si se usa una imagen remota si es necesario especificar las dimensiones ya que Next no tiene acceso a la imagen durante el proceso de build.

## **RESUMEN:**

Para crear imágenes responsivas se pueden realizar mediante el componente propio de Next.js el cual creará las mismas mediante el servidor de Node.js o también puede delegar este trabajo a servicios especializados en el mismo

> Links:
>
> - [next/image](https://nextjs.org/docs/api-reference/next/image)
> - [Image Component and Image Optimization](https://nextjs.org/docs/basic-features/image-optimization)

# Image API: configurando nuestro propio loader avanzado

---

---

# Readme NextJs

This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, create a `.env.local` file with your Contentful secrets:

```bash
cp .env.local.example .env.local
```

Create a new API Key in Contentful: "Your Space > Settings > API Keys", then replace `SPACE_ID` and `ACCESS_TOKEN` with your values.

Second, run the development server:

```bash
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.js`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

## GraphQL type generation

```bash
SPACE_ID={SPACE_ID} ACCESS_TOKEN={ACCESS_TOKEN} yarn dev
```

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
