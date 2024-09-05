# Enkel övning med `useContext` i React

I den här övningen kommer vi att skapa och använda `useContext`-hooken i React för att dela data mellan komponenter utan att behöva skicka props genom flera nivåer.

## Steg 1: Skapa en Context

Först måste vi skapa en Context genom att använda `React.createContext`. Detta gör det möjligt att dela state mellan komponenter.

```jsx
import React, { createContext, useState } from "react";

// Skapa en Context
const MyContext = createContext();

export const MyProvider = ({ children }) => {
  const [value, setValue] = useState("Hej från Context!");

  return (
    <MyContext.Provider value={{ value, setValue }}>
      {children}
    </MyContext.Provider>
  );
};

export default MyContext;
```

## Steg 2: Använd Context i en komponent

Nu när vi har skapat vår Context och en Provider kan vi använda `useContext`-hooken i andra komponenter för att få åtkomst till den delade datan.

```jsx
import React, { useContext } from "react";
import MyContext from "./MyContext";

const MyComponent = () => {
  const { value, setValue } = useContext(MyContext);

  return (
    <div>
      <h1>{value}</h1>
      <button onClick={() => setValue("Context värde uppdaterat!")}>
        Uppdatera värde
      </button>
    </div>
  );
};

export default MyComponent;
```

## Steg 3: Använd Provider för att omge komponenterna

För att `MyComponent` ska kunna få åtkomst till den delade datan måste vi se till att den är omgiven av `MyProvider`.

```jsx
import React from "react";
import ReactDOM from "react-dom";
import { MyProvider } from "./MyContext";
import MyComponent from "./MyComponent";

const App = () => {
  return (
    <MyProvider>
      <MyComponent />
    </MyProvider>
  );
};

ReactDOM.render(<App />, document.getElementById("root"));
```

## Förklaring:

1. **Skapa Context**: Vi skapar en Context med `createContext` och tillhandahåller ett initialt värde via en Provider.

2. **Använda Context**: I `MyComponent` använder vi `useContext`-hooken för att få åtkomst till värdet och en funktion för att uppdatera värdet.

3. **Omge med Provider**: Vi måste omge komponenten som ska använda Context med en Provider, så att värdet blir tillgängligt i komponenten.

Med dessa steg har du en grundläggande användning av `useContext` i React. Detta är en enkel och effektiv metod för att hantera delad state mellan komponenter utan att behöva skicka props genom många nivåer.
