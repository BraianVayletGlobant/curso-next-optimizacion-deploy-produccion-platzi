# [Curso de Next.js: Optimización y Deploy a Producción](https://platzi.com/clases/nextjs-deploy/)

### CMS usado en el proyecto: [Contentfull](https://app.contentful.com/)

- Clase1: Presentacion
- Clase2: [¿Para qué necesitamos variables de entorno?](#¿Para-qué-necesitamos-variables-de-entorno?)

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

## 📌 RESUMEN

Las variables de entorno, son la mejor forma de poder guardar contraseñas, llaves, etc. (secretos) ya que estas no son compartidas, establece una lista clara de que secretos necesita la aplicación para que no se rompa y es capaz de cargar y leer dichos valores de la lista de secretos

> Links:
>
> - [variables de entorno en node](https://www.youtube.com/watch?v=tZ3bLXoD6i0)

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
