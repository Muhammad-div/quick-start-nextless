# Start customization

### How to start the customization

Now, you can easily configure ModernMERN by making a search with `FIXME:` for making quick customization in each repository. Or, you can start adding your own code and logic in each repository.

You have access to the whole code source if you need further customization. The provided code is only example for you to start your SaaS products. The sky is the limit 🚀.

You are now ready to makes changes in ModernMERN and adapt to your own needs. You can now stop here your reading and start making your own changes.

For your information, the frontend and backend both support hot reloading. So, you can see your changes in real-time without the need to restart the server.

If you want to go further and improve your developer experience, we suggest some [local development tools](LOCAL_DEVELOPER_TOOLS.md) you can use. Or, you can return to the previous page and read the article to set up Stripe.

### Change database schema

The project uses Prisma as an ORM and the schema is located at `prisma/schema.prisma` in the backend repository. After making changes in the schema, you need to run the following command to update the database and generate the new Prisma client for TypeScript:

```bash
npx prisma db push
```

### Change the theme color

In the frontend, you can change the theme color in `tailwind.config.js` file and you need to replace the `primary` color. It'll take effect in the whole application (landing page and dashboard). Here is some example:

```ts
// Indigo
primary: {
  100: '#EBF4FF',
  200: '#C3DAFE',
  300: '#A3BFFA',
  400: '#7F9CF5',
  500: '#667EEA',
  600: '#5A67D8',
  700: '#4C51BF',
  800: '#434190',
  900: '#3C366B',
},

// Blue
primary: {
  100: '#EBF8FF',
  200: '#BEE3F8',
  300: '#90CDF4',
  400: '#63B3ED',
  500: '#4299E1',
  600: '#3182CE',
  700: '#2B6CB0',
  800: '#2C5282',
  900: '#2A4365',
},

// Teal
primary: {
  100: '#E6FFFA',
  200: '#B2F5EA',
  300: '#81E6D9',
  400: '#4FD1C5',
  500: '#38B2AC',
  600: '#319795',
  700: '#2C7A7B',
  800: '#285E61',
  900: '#234E52',
},

// Green
primary: {
  100: '#F0FFF4',
  200: '#C6F6D5',
  300: '#9AE6B4',
  400: '#68D391',
  500: '#48BB78',
  600: '#38A169',
  700: '#2F855A',
  800: '#276749',
  900: '#22543D',
},

// Purple
primary: {
  100: '#FAF5FF',
  200: '#E9D8FD',
  300: '#D6BCFA',
  400: '#B794F4',
  500: '#9F7AEA',
  600: '#805AD5',
  700: '#6B46C1',
  800: '#553C9A',
  900: '#44337A',
},

// Orange
primary: {
  100: '#FFFAF0',
  200: '#FEEBC8',
  300: '#FBD38D',
  400: '#F6AD55',
  500: '#ED8936',
  600: '#DD6B20',
  700: '#C05621',
  800: '#9C4221',
  900: '#7B341E',
},

// Red
primary: {
  100: '#FFF5F5',
  200: '#FED7D7',
  300: '#FEB2B2',
  400: '#FC8181',
  500: '#F56565',
  600: '#E53E3E',
  700: '#C53030',
  800: '#9B2C2C',
  900: '#742A2A',
},

// Pink
primary: {
  100: '#FFF5F7',
  200: '#FED7E2',
  300: '#FBB6CE',
  400: '#F687B3',
  500: '#ED64A6',
  600: '#D53F8C',
  700: '#B83280',
  800: '#97266D',
  900: '#702459',
},

// You can also use your own color to match your brand
```

After changing the color, you need to delete `.next` folder cache and restart the frontend `npm run dev` to see the changes.
