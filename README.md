# Programação Mible usando Firebase

## ![alt text](image.png)

# Banco de Dados online 

## ![alt text](image-1.png)

### FIREBASECONFIG.JS

```bash
    npm install firebase
```

# Programe toda linha de comando necessária

```js

    import { inicializeApp } from 'firebase/app';
import { getFirestore } from 'firebase/firestore';
import { getAuth } from 'firebase/auth'

const firebaseConfig = {
    apiKey: "AIzaSyCHM_20VLoRldkin3cSRmyjjq-4ftsZPs8",
    authDomain: "pets-689f2.firebaseapp.com",
    projectId: "pets-689f2",
    storageBucket: "pets-689f2.appspot.com",
    messagingSenderId: "313132279920",
    appId: "1:313132279920:web:de70d899fb42554dc06cb5",
    measurementId: "G-YW0ZSBW2MT"
  };
  
  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const analytics = getAnalytics(app);

  const db = getFirestore(app);

  const auth = getAuth(app);

  export { db, auth };

```

### APP.JS

```js

   import React, { useState } from "react";
import { StyleSheet, Text, View, Button, TextInput, FlatList, Image } from "react-native";
import { db } from "./firebaseconfig";
import { collection, addDoc, getDocs } from "firebase/firestore";


export default function App() {
  const [namePet, SetNamePet] = useState("");
  const [tipoPet, setTipoPet] = useState("");
  const [pets, setPets] = useState([]);
  const [loading, setLoading] = useState(false);

  const adicionaPet = async () => {
    try {
      setLoading(true);
      await addDoc(collection(db, "pets"), {
        nome: namePet,
        tipo: tipoPet
      });
      alert("Pet adicionadp com sucesso!");
      SetNamePet('');
      setTipoPet('');
      fetchPets();
    } catch (e) {
      console.error("Erro ao adicionar pet", e);
    } finally {
      setLoading(false);
    }
  };

  const fetchPets = async () => {
    try {
      const querySnapshot = await getDocs(collection(db, "pets"));
      const petlist = querySnapshot.docs.map(doc => doc.data());
      setPets(petlist);
    } catch (e) {
      console.error("Erro ao buscar pets", e);
    }
  };

  return (
    < View style={styles.container}>

      <Text style={styles.title}>Pets SENAI</Text>

      <Text style={style.lable}>Nome do Pet</Text>

      <TextInput
        style={styles.input}
        placeholder="Digite o nome do pet"
        value={namePet}
        onChangeText={SetNamePet}
      />

      <Button
        title={loading ? "Adicionando..." : "Adicionar Pet"}
        onPress={adicionarPet}
        color="#6b8e23"
      />

      <Text style={styles.label}>Lista de Pets</Text>
      <FlatList
        data={pets}
        keyExtractor={(item, index) => index.toString()}
        renderItem={({ item }) => (
          <View style={styles.petItem}>
            <image
              source={{ uri: 'https://via.placeholder.com/100' }}
              style={styles.petImage}
            />
          <view>
            <Text style={styles.petName}>{item.nome}</Text>
            <Text style={styles.petType}>{item.tipo}</Text>
          </view>
          </View>
      )}
        style={styles.petList}
        />
          </View>
        );
        }

        const styles = StyleSheet.create({
          container: {
            flex: 1,
            backgroundColor: '#f0f8ff',
            padding: 20,
          },
          title: {
            fontSize: 32,
            fontWeight: 'bold',
            color: '4682b4',
            textAlign: 'center',
            marginBottom: 20,
          },
          label: {
            fontSize: 18,
            marginBottom: 5,
            color: '#333',
          },
        
          input: {
            width: '100%',
            padding: 10,
            marginBotton: 15,
            borderWidth: 1,
            borderColor: '#ccc',
            borderRadius: 5,
            backgroundColor: '#fff',
          },
        
          Button: {
            backgroundColor: '#6b8e23',
            color: '#fff',
            padding: 10,borderRadius: 5,
          },
        
          sectionTitle: {
            fontSize: 24,
            fontWeight: 'bold',
            color: '#4682b4',
            marginTop: 20,
            marginBottom: 10,
          },
          petList: {
            marginTop: 10,
          },
          petItem: {
            flexDirection: 'row',
            alignItems: 'center',
            backgroundColor: '#fff',
            padding: 10,
            borderRadius: 5,
            marginBottom: 10,
            shadowColor: '#000',
            shadowOffset: { width: 0, height: 2 },
            shadowOpacity: 0.2,
            shadowRadius: 2,
            elevation: 3,
          },
          petImage: {
            width: 50,
            height: 50,
            borderRadius: 25,
            marginRight: 15,
          },
          petName: {
            fontSize: 18,
            fontWeight: 'bold',
            color: '#333',
          },
          petType: {
            fontSize: 16,
            color: '#555',
          },
        });

```

# BANCO DE DADOS 

```JS
        rules_version = '2';

    service cloud.firestore {
    match /databases/{database}/documents {
        match /{document=**} {
        allow read, write: if true; //ALTERAR PARA TRUE 
        }
    }
    }

```

## Após realizar toda linha de programação executar os seguintes comandos

- instalar dependências

    ```bash
    npx create-expo-app petshop --template blank
    ```

- rodar o codiga para abrir o servidor
    
    ```bash
    yarn run web
    ```

    ```bash
    yarn add react-native-web react-dom @expo/metro-runtime
    ```


