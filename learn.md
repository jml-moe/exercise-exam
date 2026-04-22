# React Native Core Components — Cheat Sheet & Contoh Kode

> Source: https://reactnative.dev/docs/components-and-apis  
> Semua komponen diimport dari `'react-native'` kecuali ada catatan khusus.

---

## Instalasi Dependensi yang Diperlukan

```bash
# Wajib untuk SafeAreaView (dipakai di banyak contoh resmi)
npm install react-native-safe-area-context

# Untuk navigasi (opsional, jika butuh)
npm install @react-navigation/native
```

---

## BASIC COMPONENTS

---

### 1. `View`

> Container utama untuk layout. Setara dengan `<div>` di HTML.

**Props penting:** `style`, `onLayout`, `pointerEvents`

```jsx
import React from "react";
import { View, Text, StyleSheet } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <View style={styles.box1} />
      <View style={styles.box2} />
      <Text>Halo dari dalam View!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: "row",
    justifyContent: "center",
    alignItems: "center",
    padding: 16,
  },
  box1: { width: 50, height: 50, backgroundColor: "red", margin: 8 },
  box2: { width: 50, height: 50, backgroundColor: "blue", margin: 8 },
});
```

---

### 2. `Text`

> Komponen untuk menampilkan teks.

**Props penting:** `style`, `numberOfLines`, `onPress`, `ellipsizeMode`

```jsx
import React from "react";
import { Text, StyleSheet } from "react-native";

export default function App() {
  return (
    <>
      <Text style={styles.header}>Judul Besar</Text>
      <Text style={styles.body} numberOfLines={2}>
        Ini adalah paragraf panjang yang akan dipotong setelah 2 baris jika
        teksnya terlalu panjang untuk muat.
      </Text>
      <Text onPress={() => alert("Teks diklik!")}>Klik saya!</Text>
    </>
  );
}

const styles = StyleSheet.create({
  header: { fontSize: 24, fontWeight: "bold", color: "#333" },
  body: { fontSize: 14, color: "#666", lineHeight: 22 },
});
```

---

### 3. `Image`

> Komponen untuk menampilkan gambar (lokal maupun dari URL).

**Props penting:** `source`, `style`, `resizeMode`, `onLoad`, `onError`

```jsx
import React from "react";
import { Image, StyleSheet, View } from "react-native";

export default function App() {
  return (
    <View>
      {/* Gambar dari URL */}
      <Image
        source={{ uri: "https://reactnative.dev/img/tiny_logo.png" }}
        style={styles.logo}
        resizeMode="contain"
      />

      {/* Gambar lokal */}
      {/* <Image source={require('./assets/logo.png')} style={styles.logo} /> */}
    </View>
  );
}

const styles = StyleSheet.create({
  logo: {
    width: 100,
    height: 100,
    borderRadius: 8,
  },
});
```

---

### 4. `TextInput`

> Komponen input teks dari keyboard.

**Props penting:** `value`, `onChangeText`, `placeholder`, `secureTextEntry`, `keyboardType`, `multiline`

```jsx
import React, { useState } from "react";
import { TextInput, Text, View, StyleSheet } from "react-native";

export default function App() {
  const [nama, setNama] = useState("");
  const [password, setPassword] = useState("");

  return (
    <View style={styles.container}>
      <TextInput
        style={styles.input}
        placeholder="Masukkan nama..."
        value={nama}
        onChangeText={setNama}
      />
      <TextInput
        style={styles.input}
        placeholder="Password"
        value={password}
        onChangeText={setPassword}
        secureTextEntry={true}
        keyboardType="default"
      />
      <Text>Nama: {nama}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { padding: 16 },
  input: {
    borderWidth: 1,
    borderColor: "#ccc",
    borderRadius: 8,
    padding: 10,
    marginBottom: 12,
  },
});
```

---

### 5. `ScrollView`

> Container yang bisa di-scroll, cocok untuk konten pendek-menengah.

**Props penting:** `horizontal`, `showsVerticalScrollIndicator`, `refreshControl`, `onScroll`

```jsx
import React from "react";
import { ScrollView, Text, StyleSheet, View } from "react-native";

export default function App() {
  return (
    <ScrollView style={styles.container}>
      {Array.from({ length: 20 }, (_, i) => (
        <View key={i} style={styles.card}>
          <Text>Item ke-{i + 1}</Text>
        </View>
      ))}
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1 },
  card: {
    backgroundColor: "#f0f0f0",
    padding: 16,
    marginVertical: 4,
    marginHorizontal: 8,
    borderRadius: 8,
  },
});
```

---

### 6. `Pressable`

> Wrapper komponen untuk mendeteksi sentuhan. Pengganti modern dari Touchable\*.

**Props penting:** `onPress`, `onLongPress`, `onPressIn`, `onPressOut`, `style` (bisa function)

```jsx
import React from "react";
import { Pressable, Text, StyleSheet } from "react-native";

export default function App() {
  return (
    <Pressable
      onPress={() => alert("Ditekan!")}
      onLongPress={() => alert("Ditekan lama!")}
      style={({ pressed }) => [styles.button, pressed && styles.buttonPressed]}
    >
      <Text style={styles.text}>Tekan Saya</Text>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: "#007AFF",
    padding: 14,
    borderRadius: 8,
    alignItems: "center",
  },
  buttonPressed: {
    backgroundColor: "#0055CC",
    opacity: 0.8,
  },
  text: { color: "#fff", fontSize: 16, fontWeight: "bold" },
});
```

---

### 7. `StyleSheet`

> Abstraksi mirip CSS untuk membuat style. Lebih performant dari inline style.

**Method penting:** `StyleSheet.create()`, `StyleSheet.flatten()`

```jsx
import React from "react";
import { StyleSheet, Text, View } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>StyleSheet Example</Text>
      {/* Menggabungkan beberapa style */}
      <Text style={[styles.title, styles.highlighted]}>Highlighted Text</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
  title: {
    fontSize: 20,
    color: "#333",
  },
  highlighted: {
    backgroundColor: "yellow",
    fontWeight: "bold",
  },
});
```

---

## USER INTERFACE

---

### 8. `Button`

> Tombol sederhana yang tampil konsisten di semua platform.

**Props penting:** `title` (wajib), `onPress` (wajib), `color`, `disabled`

```jsx
import React from "react";
import { Button, View, Alert, StyleSheet } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Button
        title="Tekan Saya"
        onPress={() => Alert.alert("Tombol ditekan!")}
        color="#841584"
      />
      <Button title="Tombol Disabled" onPress={() => {}} disabled={true} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", gap: 12, padding: 16 },
});
```

---

### 9. `Switch`

> Toggle boolean (on/off). Setara dengan toggle wifi di settings.

**Props penting:** `value` (wajib), `onValueChange` (wajib), `trackColor`, `thumbColor`, `disabled`

```jsx
import React, { useState } from "react";
import { Switch, View, Text, StyleSheet } from "react-native";

export default function App() {
  const [isEnabled, setIsEnabled] = useState(false);

  return (
    <View style={styles.container}>
      <Text>Mode Gelap: {isEnabled ? "ON" : "OFF"}</Text>
      <Switch
        value={isEnabled}
        onValueChange={(val) => setIsEnabled(val)}
        trackColor={{ false: "#767577", true: "#81b0ff" }}
        thumbColor={isEnabled ? "#007AFF" : "#f4f3f4"}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    gap: 12,
  },
});
```

---

## LIST VIEWS

---

### 10. `FlatList`

> List performant untuk daftar panjang. Hanya render item yang terlihat di layar.

**Props penting:** `data` (wajib), `renderItem` (wajib), `keyExtractor`, `horizontal`, `ListHeaderComponent`, `ListEmptyComponent`, `extraData`

```jsx
import React from "react";
import { FlatList, View, Text, StyleSheet } from "react-native";

const DATA = [
  { id: "1", title: "Item Pertama" },
  { id: "2", title: "Item Kedua" },
  { id: "3", title: "Item Ketiga" },
  { id: "4", title: "Item Keempat" },
  { id: "5", title: "Item Kelima" },
];

const ItemCard = ({ title }) => (
  <View style={styles.card}>
    <Text>{title}</Text>
  </View>
);

export default function App() {
  return (
    <FlatList
      data={DATA}
      renderItem={({ item }) => <ItemCard title={item.title} />}
      keyExtractor={(item) => item.id}
      ListHeaderComponent={<Text style={styles.header}>Daftar Item</Text>}
      ListEmptyComponent={<Text>Tidak ada data</Text>}
    />
  );
}

const styles = StyleSheet.create({
  card: {
    backgroundColor: "#f9f9f9",
    padding: 16,
    marginVertical: 4,
    marginHorizontal: 12,
    borderRadius: 8,
    borderWidth: 1,
    borderColor: "#ddd",
  },
  header: { fontSize: 20, fontWeight: "bold", padding: 12 },
});
```

---

### 11. `SectionList`

> Seperti FlatList tapi dengan section/grup dan header per section.

**Props penting:** `sections` (wajib), `renderItem` (wajib), `renderSectionHeader`, `keyExtractor`

```jsx
import React from "react";
import { SectionList, View, Text, StyleSheet } from "react-native";

const DATA = [
  {
    title: "Buah-buahan",
    data: ["Apel", "Mangga", "Pisang"],
  },
  {
    title: "Sayuran",
    data: ["Wortel", "Bayam", "Brokoli"],
  },
];

export default function App() {
  return (
    <SectionList
      sections={DATA}
      keyExtractor={(item, index) => item + index}
      renderItem={({ item }) => (
        <View style={styles.item}>
          <Text>{item}</Text>
        </View>
      )}
      renderSectionHeader={({ section: { title } }) => (
        <Text style={styles.header}>{title}</Text>
      )}
    />
  );
}

const styles = StyleSheet.create({
  item: { padding: 12, paddingLeft: 24 },
  header: {
    backgroundColor: "#eee",
    padding: 12,
    fontWeight: "bold",
    fontSize: 16,
  },
});
```

---

## OTHERS

---

### 12. `ActivityIndicator`

> Menampilkan loading spinner (indikator loading bulat berputar).

**Props penting:** `size`, `color`, `animating`

```jsx
import React, { useState, useEffect } from "react";
import { ActivityIndicator, View, Text, StyleSheet } from "react-native";

export default function App() {
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    // Simulasi loading data selama 3 detik
    setTimeout(() => setIsLoading(false), 3000);
  }, []);

  return (
    <View style={styles.container}>
      {isLoading ? (
        <>
          <ActivityIndicator size="large" color="#007AFF" />
          <Text style={styles.text}>Memuat data...</Text>
        </>
      ) : (
        <Text style={styles.text}>Data berhasil dimuat!</Text>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
  text: { marginTop: 12, fontSize: 16 },
});
```

---

### 13. `Alert`

> BUKAN komponen JSX — ini adalah API yang dipanggil sebagai fungsi!

**Method:** `Alert.alert(title, message, buttons, options)`

```jsx
import React from "react";
import { Alert, Button, View, StyleSheet } from "react-native";

export default function App() {
  const showBasicAlert = () => {
    Alert.alert("Perhatian", "Ini adalah alert sederhana.");
  };

  const showConfirmAlert = () => {
    Alert.alert("Hapus Data", "Apakah kamu yakin ingin menghapus data ini?", [
      {
        text: "Batal",
        onPress: () => console.log("Dibatalkan"),
        style: "cancel", // iOS: tampilkan sebagai cancel button
      },
      {
        text: "Hapus",
        onPress: () => console.log("Data dihapus!"),
        style: "destructive", // iOS: warna merah
      },
    ]);
  };

  return (
    <View style={styles.container}>
      <Button title="Alert Biasa" onPress={showBasicAlert} />
      <Button title="Alert Konfirmasi" onPress={showConfirmAlert} color="red" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", gap: 12, padding: 24 },
});
```

---

### 14. `Modal`

> Layar overlay yang muncul di atas konten utama.

**Props penting:** `visible` (wajib), `animationType`, `transparent`, `onRequestClose`

```jsx
import React, { useState } from "react";
import { Modal, View, Text, Pressable, StyleSheet, Alert } from "react-native";

export default function App() {
  const [modalVisible, setModalVisible] = useState(false);

  return (
    <View style={styles.container}>
      {/* Tombol untuk buka modal */}
      <Pressable
        style={styles.openButton}
        onPress={() => setModalVisible(true)}
      >
        <Text style={styles.buttonText}>Buka Modal</Text>
      </Pressable>

      {/* Definisi Modal */}
      <Modal
        animationType="slide" // 'none' | 'slide' | 'fade'
        transparent={true}
        visible={modalVisible}
        onRequestClose={() => {
          Alert.alert("Modal ditutup via back button");
          setModalVisible(false);
        }}
      >
        <View style={styles.overlay}>
          <View style={styles.modalBox}>
            <Text style={styles.modalTitle}>Halo dari Modal!</Text>
            <Text style={styles.modalBody}>
              Ini adalah konten di dalam modal.
            </Text>
            <Pressable
              style={styles.closeButton}
              onPress={() => setModalVisible(false)}
            >
              <Text style={styles.buttonText}>Tutup Modal</Text>
            </Pressable>
          </View>
        </View>
      </Modal>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
  overlay: {
    flex: 1,
    backgroundColor: "rgba(0,0,0,0.5)",
    justifyContent: "center",
    alignItems: "center",
  },
  modalBox: {
    backgroundColor: "white",
    borderRadius: 16,
    padding: 24,
    width: "80%",
    alignItems: "center",
    elevation: 8,
    shadowColor: "#000",
    shadowOpacity: 0.25,
    shadowRadius: 8,
  },
  modalTitle: { fontSize: 20, fontWeight: "bold", marginBottom: 8 },
  modalBody: {
    fontSize: 14,
    color: "#666",
    marginBottom: 20,
    textAlign: "center",
  },
  openButton: {
    backgroundColor: "#007AFF",
    padding: 14,
    borderRadius: 8,
  },
  closeButton: {
    backgroundColor: "#FF3B30",
    padding: 12,
    borderRadius: 8,
    width: "100%",
    alignItems: "center",
  },
  buttonText: { color: "white", fontWeight: "bold", fontSize: 16 },
});
```

---

### 15. `KeyboardAvoidingView`

> Otomatis menggeser konten agar tidak tertutup keyboard virtual.

**Props penting:** `behavior` (`'padding'` | `'height'` | `'position'`), `keyboardVerticalOffset`

> Gunakan `Platform.OS === 'ios' ? 'padding' : 'height'` karena behavior beda di iOS dan Android.

```jsx
import React, { useState } from "react";
import {
  KeyboardAvoidingView,
  TextInput,
  Text,
  Platform,
  StyleSheet,
  View,
  Button,
} from "react-native";

export default function App() {
  const [pesan, setPesan] = useState("");

  return (
    <KeyboardAvoidingView
      style={styles.container}
      behavior={Platform.OS === "ios" ? "padding" : "height"}
    >
      <View style={styles.inner}>
        <Text style={styles.title}>Form Login</Text>

        <TextInput
          style={styles.input}
          placeholder="Email"
          keyboardType="email-address"
        />
        <TextInput
          style={styles.input}
          placeholder="Password"
          secureTextEntry
        />
        <TextInput
          style={[styles.input, { height: 80 }]}
          placeholder="Pesan..."
          value={pesan}
          onChangeText={setPesan}
          multiline
        />

        <Button title="Submit" onPress={() => {}} />
      </View>
    </KeyboardAvoidingView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1 },
  inner: {
    flex: 1,
    justifyContent: "flex-end",
    padding: 24,
  },
  title: { fontSize: 24, fontWeight: "bold", marginBottom: 20 },
  input: {
    borderWidth: 1,
    borderColor: "#ccc",
    borderRadius: 8,
    padding: 12,
    marginBottom: 12,
    backgroundColor: "#fff",
  },
});
```

---

### 16. `Dimensions`

> API untuk mendapatkan ukuran layar device. Berguna untuk layout responsif.

**Method:** `Dimensions.get('window')` atau `Dimensions.get('screen')`

> 'window' = ukuran area app (tanpa status bar di Android). 'screen' = ukuran fisik layar.

```jsx
import React from "react";
import { Dimensions, View, Text, StyleSheet } from "react-native";

const { width, height } = Dimensions.get("window");

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Lebar layar: {width}px</Text>
      <Text style={styles.text}>Tinggi layar: {height}px</Text>

      {/* Contoh penggunaan: kotak 50% lebar layar */}
      <View style={[styles.box, { width: width * 0.5 }]}>
        <Text>50% dari lebar layar</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    gap: 12,
  },
  text: { fontSize: 16 },
  box: {
    height: 100,
    backgroundColor: "#007AFF",
    justifyContent: "center",
    alignItems: "center",
    borderRadius: 8,
  },
});
```

---

### 17. `StatusBar`

> Mengontrol tampilan status bar (area jam, baterai, sinyal) di bagian atas HP.

**Props penting:** `barStyle`, `backgroundColor` (Android), `hidden`, `translucent`

```jsx
import React, { useState } from "react";
import { StatusBar, View, Button, StyleSheet } from "react-native";

export default function App() {
  const [isDark, setIsDark] = useState(false);

  return (
    <View
      style={[
        styles.container,
        { backgroundColor: isDark ? "#1a1a1a" : "#fff" },
      ]}
    >
      {/* barStyle: 'default' | 'light-content' | 'dark-content' */}
      <StatusBar
        barStyle={isDark ? "light-content" : "dark-content"}
        backgroundColor={isDark ? "#1a1a1a" : "#ffffff"}
      />
      <Button
        title={`Mode: ${isDark ? "Gelap" : "Terang"}`}
        onPress={() => setIsDark(!isDark)}
        color={isDark ? "#fff" : "#333"}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
});
```

---

### 18. `RefreshControl`

> Fitur pull-to-refresh. Hanya dipakai sebagai prop di dalam `ScrollView` atau `FlatList`.

**Props penting:** `refreshing` (wajib), `onRefresh` (wajib), `colors`, `tintColor`

```jsx
import React, { useState, useCallback } from "react";
import {
  ScrollView,
  RefreshControl,
  Text,
  View,
  StyleSheet,
} from "react-native";

export default function App() {
  const [refreshing, setRefreshing] = useState(false);
  const [data, setData] = useState(["Item 1", "Item 2", "Item 3"]);

  const onRefresh = useCallback(() => {
    setRefreshing(true);
    // Simulasi fetch data baru
    setTimeout(() => {
      setData(["Item Baru 1", "Item Baru 2", "Item Baru 3", "Item Baru 4"]);
      setRefreshing(false);
    }, 2000);
  }, []);

  return (
    <ScrollView
      style={styles.container}
      refreshControl={
        <RefreshControl
          refreshing={refreshing}
          onRefresh={onRefresh}
          colors={["#007AFF"]} // Android: warna spinner
          tintColor="#007AFF" // iOS: warna spinner
        />
      }
    >
      {data.map((item, index) => (
        <View key={index} style={styles.card}>
          <Text>{item}</Text>
        </View>
      ))}
      <Text style={styles.hint}>Tarik ke bawah untuk refresh</Text>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: "#f5f5f5" },
  card: {
    backgroundColor: "#fff",
    padding: 16,
    margin: 8,
    borderRadius: 8,
    elevation: 2,
  },
  hint: { textAlign: "center", color: "#999", padding: 16 },
});
```

---

### 19. `Animated`

> Library untuk membuat animasi yang smooth dan powerful.

**Method penting:** `Animated.Value()`, `Animated.timing()`, `Animated.spring()`, `Animated.loop()`

```jsx
import React, { useRef, useEffect } from "react";
import { Animated, View, Button, StyleSheet } from "react-native";

export default function App() {
  const fadeAnim = useRef(new Animated.Value(0)).current; // opacity awal: 0
  const slideAnim = useRef(new Animated.Value(-100)).current; // posisi awal: -100

  const animateIn = () => {
    // Jalankan dua animasi sekaligus (parallel)
    Animated.parallel([
      Animated.timing(fadeAnim, {
        toValue: 1,
        duration: 500,
        useNativeDriver: true,
      }),
      Animated.timing(slideAnim, {
        toValue: 0,
        duration: 500,
        useNativeDriver: true,
      }),
    ]).start();
  };

  const animateOut = () => {
    Animated.parallel([
      Animated.timing(fadeAnim, {
        toValue: 0,
        duration: 300,
        useNativeDriver: true,
      }),
      Animated.timing(slideAnim, {
        toValue: -100,
        duration: 300,
        useNativeDriver: true,
      }),
    ]).start();
  };

  return (
    <View style={styles.container}>
      <Animated.View
        style={[
          styles.box,
          {
            opacity: fadeAnim,
            transform: [{ translateY: slideAnim }],
          },
        ]}
      />
      <View style={styles.buttons}>
        <Button title="Animasi Masuk" onPress={animateIn} />
        <Button title="Animasi Keluar" onPress={animateOut} color="red" />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
  box: {
    width: 150,
    height: 150,
    backgroundColor: "#007AFF",
    borderRadius: 12,
    marginBottom: 32,
  },
  buttons: { gap: 12 },
});
```

---

### 20. `Linking`

> API untuk membuka URL eksternal, deep link, atau aplikasi lain.

**Method:** `Linking.openURL()`, `Linking.canOpenURL()`, `Linking.getInitialURL()`

```jsx
import React from "react";
import { Linking, Button, View, Alert, StyleSheet } from "react-native";

export default function App() {
  const openWebsite = async () => {
    const url = "https://reactnative.dev";
    const canOpen = await Linking.canOpenURL(url);
    if (canOpen) {
      await Linking.openURL(url);
    } else {
      Alert.alert("Error", "Tidak bisa membuka URL ini");
    }
  };

  const openEmail = () => {
    Linking.openURL("mailto:hello@example.com?subject=Halo&body=Apa kabar?");
  };

  const openPhone = () => {
    Linking.openURL("tel:+6281234567890");
  };

  return (
    <View style={styles.container}>
      <Button title="Buka Website" onPress={openWebsite} />
      <Button title="Kirim Email" onPress={openEmail} />
      <Button title="Telepon" onPress={openPhone} color="green" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", gap: 12, padding: 24 },
});
```

---

### 21. `PixelRatio`

> API untuk mendapatkan pixel density layar device.

**Method:** `PixelRatio.get()`, `PixelRatio.getPixelSizeForLayoutSize()`, `PixelRatio.roundToNearestPixel()`

```jsx
import React from "react";
import { PixelRatio, Text, View, StyleSheet } from "react-native";

const ratio = PixelRatio.get(); // contoh: 2 (Retina), 3 (iPhone Plus)
const fontSize = PixelRatio.roundToNearestPixel(16); // ukuran font yang tepat

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Pixel Ratio: {ratio}</Text>
      <Text>Font size (rounded): {fontSize}px</Text>
      <Text>
        100dp = {PixelRatio.getPixelSizeForLayoutSize(100)} piksel fisik
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    gap: 8,
  },
});
```

---

## TOUCHABLE COMPONENTS (Lama, tapi masih dipakai)

---

### 22. `TouchableOpacity`

> Komponen yang memberikan efek opacity saat ditekan. Paling sering dipakai.

```jsx
import React from "react";
import { TouchableOpacity, Text, StyleSheet, Alert } from "react-native";

export default function App() {
  return (
    <TouchableOpacity
      style={styles.button}
      activeOpacity={0.7} // default: 0.2
      onPress={() => Alert.alert("Ditekan!")}
    >
      <Text style={styles.text}>Tombol TouchableOpacity</Text>
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: "#FF9500",
    padding: 14,
    borderRadius: 8,
    alignItems: "center",
    margin: 24,
  },
  text: { color: "white", fontWeight: "bold", fontSize: 16 },
});
```

---

### 23. `TouchableHighlight`

> Memberikan efek highlight warna saat ditekan.

```jsx
import React from "react";
import { TouchableHighlight, Text, StyleSheet, Alert } from "react-native";

export default function App() {
  return (
    <TouchableHighlight
      style={styles.button}
      underlayColor="#005EB8" // warna saat ditekan
      onPress={() => Alert.alert("Ditekan!")}
    >
      <Text style={styles.text}>Tombol TouchableHighlight</Text>
    </TouchableHighlight>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: "#007AFF",
    padding: 14,
    borderRadius: 8,
    alignItems: "center",
    margin: 24,
  },
  text: { color: "white", fontWeight: "bold", fontSize: 16 },
});
```

---

### 24. `TouchableWithoutFeedback`

> Komponen touchable TANPA efek visual. Gunakan untuk area tap tersembunyi.

```jsx
import React from "react";
import {
  TouchableWithoutFeedback,
  View,
  Text,
  StyleSheet,
  Alert,
} from "react-native";

export default function App() {
  return (
    // Membungkus View biasa — tap tidak ada efek visual
    <TouchableWithoutFeedback onPress={() => Alert.alert("Area ini diklik!")}>
      <View style={styles.area}>
        <Text>Tap di mana saja di kotak ini (tidak ada efek visual)</Text>
      </View>
    </TouchableWithoutFeedback>
  );
}

const styles = StyleSheet.create({
  area: {
    backgroundColor: "#e0e0e0",
    padding: 24,
    margin: 24,
    borderRadius: 8,
    alignItems: "center",
  },
});
```

---

### 25. `ImageBackground`

> Menampilkan gambar sebagai background dengan children di atasnya.

```jsx
import React from "react";
import { ImageBackground, Text, StyleSheet, View } from "react-native";

export default function App() {
  return (
    <ImageBackground
      source={{ uri: "https://reactnative.dev/img/back_hero.png" }}
      style={styles.bgImage}
      resizeMode="cover"
    >
      <View style={styles.overlay}>
        <Text style={styles.title}>Judul di atas gambar</Text>
        <Text style={styles.subtitle}>Subtitle teks</Text>
      </View>
    </ImageBackground>
  );
}

const styles = StyleSheet.create({
  bgImage: { flex: 1, justifyContent: "center" },
  overlay: {
    backgroundColor: "rgba(0,0,0,0.4)",
    padding: 24,
    alignItems: "center",
  },
  title: { color: "white", fontSize: 28, fontWeight: "bold" },
  subtitle: { color: "#ddd", fontSize: 16, marginTop: 8 },
});
```

---

## ANDROID-SPECIFIC

---

### 26. `ToastAndroid` _(Android only)_

> Menampilkan pesan singkat (toast) di Android.

```jsx
import React from "react";
import { ToastAndroid, Button, Platform, Alert, View } from "react-native";

export default function App() {
  const showToast = () => {
    if (Platform.OS === "android") {
      ToastAndroid.show("Ini adalah Toast!", ToastAndroid.SHORT);
      // ToastAndroid.LONG untuk durasi lebih lama
    } else {
      Alert.alert("Info", "Toast hanya tersedia di Android");
    }
  };

  return (
    <View style={{ flex: 1, justifyContent: "center", padding: 24 }}>
      <Button title="Tampilkan Toast" onPress={showToast} />
    </View>
  );
}
```

---

## iOS-SPECIFIC

### `ActionSheetIOS` _(iOS only)_

> Menampilkan action sheet (menu pilihan dari bawah) di iOS.

```jsx
import { ActionSheetIOS, Button, Platform, Alert, View } from "react-native";

const showActionSheet = () => {
  if (Platform.OS === "ios") {
    ActionSheetIOS.showActionSheetWithOptions(
      {
        options: ["Batal", "Hapus", "Edit"],
        destructiveButtonIndex: 1, // index tombol merah (berbahaya)
        cancelButtonIndex: 0,
      },
      (buttonIndex) => {
        if (buttonIndex === 1) console.log("Hapus dipilih");
        if (buttonIndex === 2) console.log("Edit dipilih");
      },
    );
  }
};
```

---

## QUICK REFERENCE — Props Paling Penting

| Komponen               | Props Kunci                                                 |
| ---------------------- | ----------------------------------------------------------- |
| `View`                 | `style`, `onLayout`                                         |
| `Text`                 | `style`, `numberOfLines`, `onPress`                         |
| `Image`                | `source`, `style`, `resizeMode`                             |
| `TextInput`            | `value`, `onChangeText`, `placeholder`, `secureTextEntry`   |
| `ScrollView`           | `horizontal`, `refreshControl`                              |
| `Pressable`            | `onPress`, `onLongPress`, `style` (fn)                      |
| `Button`               | `title`, `onPress`, `color`, `disabled`                     |
| `Switch`               | `value`, `onValueChange`, `trackColor`                      |
| `FlatList`             | `data`, `renderItem`, `keyExtractor`                        |
| `SectionList`          | `sections`, `renderItem`, `renderSectionHeader`             |
| `ActivityIndicator`    | `size`, `color`, `animating`                                |
| `Alert`                | `Alert.alert(title, msg, buttons)` — bukan JSX!             |
| `Modal`                | `visible`, `animationType`, `transparent`, `onRequestClose` |
| `KeyboardAvoidingView` | `behavior` (ios: 'padding', android: 'height')              |
| `Dimensions`           | `Dimensions.get('window')` → `{width, height}`              |
| `StatusBar`            | `barStyle`, `backgroundColor`                               |
| `RefreshControl`       | `refreshing`, `onRefresh` — dipakai di ScrollView           |
| `Animated`             | `Animated.Value()`, `Animated.timing().start()`             |

---

## CONTOH APP LENGKAP (Menggabungkan Banyak Komponen)

```jsx
import React, { useState, useCallback } from "react";
import {
  View,
  Text,
  TextInput,
  FlatList,
  ActivityIndicator,
  RefreshControl,
  Modal,
  Pressable,
  Alert,
  StatusBar,
  StyleSheet,
  Switch,
} from "react-native";

const DUMMY_DATA = [
  { id: "1", title: "Belajar React Native" },
  { id: "2", title: "Kuasai Core Components" },
  { id: "3", title: "Ujian Besok Lulus" },
];

export default function App() {
  const [search, setSearch] = useState("");
  const [loading, setLoading] = useState(false);
  const [refreshing, setRefreshing] = useState(false);
  const [modalVisible, setModalVisible] = useState(false);
  const [darkMode, setDarkMode] = useState(false);

  const onRefresh = useCallback(() => {
    setRefreshing(true);
    setTimeout(() => setRefreshing(false), 1500);
  }, []);

  const filtered = DUMMY_DATA.filter((item) =>
    item.title.toLowerCase().includes(search.toLowerCase()),
  );

  return (
    <View style={[styles.container, darkMode && styles.dark]}>
      <StatusBar barStyle={darkMode ? "light-content" : "dark-content"} />

      {/* Header */}
      <View style={styles.header}>
        <Text style={[styles.title, darkMode && styles.lightText]}>
          Todo App
        </Text>
        <Switch value={darkMode} onValueChange={setDarkMode} />
      </View>

      {/* Search */}
      <TextInput
        style={styles.input}
        placeholder="Cari..."
        value={search}
        onChangeText={setSearch}
      />

      {/* Loading */}
      {loading && <ActivityIndicator size="large" color="#007AFF" />}

      {/* List */}
      <FlatList
        data={filtered}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <Pressable
            style={styles.card}
            onPress={() => Alert.alert("Dipilih", item.title)}
          >
            <Text>{item.title}</Text>
          </Pressable>
        )}
        refreshControl={
          <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
        }
        ListEmptyComponent={<Text style={styles.empty}>Tidak ada hasil</Text>}
      />

      {/* Tombol buka modal */}
      <Pressable style={styles.fab} onPress={() => setModalVisible(true)}>
        <Text style={styles.fabText}>+ Tambah</Text>
      </Pressable>

      {/* Modal */}
      <Modal visible={modalVisible} animationType="slide" transparent>
        <View style={styles.overlay}>
          <View style={styles.modalBox}>
            <Text style={styles.modalTitle}>Form Tambah Item</Text>
            <TextInput style={styles.input} placeholder="Nama item baru..." />
            <Pressable
              style={styles.button}
              onPress={() => setModalVisible(false)}
            >
              <Text style={styles.buttonText}>Simpan & Tutup</Text>
            </Pressable>
          </View>
        </View>
      </Modal>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: "#f5f5f5", padding: 16 },
  dark: { backgroundColor: "#1a1a1a" },
  lightText: { color: "#fff" },
  header: {
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    marginBottom: 12,
  },
  title: { fontSize: 24, fontWeight: "bold" },
  input: {
    borderWidth: 1,
    borderColor: "#ccc",
    borderRadius: 8,
    padding: 10,
    marginBottom: 12,
    backgroundColor: "#fff",
  },
  card: {
    backgroundColor: "#fff",
    padding: 16,
    marginVertical: 4,
    borderRadius: 8,
    elevation: 1,
  },
  empty: { textAlign: "center", color: "#999", marginTop: 24 },
  fab: {
    backgroundColor: "#007AFF",
    padding: 16,
    borderRadius: 12,
    alignItems: "center",
    margin: 8,
  },
  fabText: { color: "#fff", fontWeight: "bold", fontSize: 16 },
  overlay: {
    flex: 1,
    backgroundColor: "rgba(0,0,0,0.5)",
    justifyContent: "flex-end",
  },
  modalBox: {
    backgroundColor: "#fff",
    borderTopLeftRadius: 20,
    borderTopRightRadius: 20,
    padding: 24,
  },
  modalTitle: { fontSize: 18, fontWeight: "bold", marginBottom: 16 },
  button: {
    backgroundColor: "#34C759",
    padding: 14,
    borderRadius: 8,
    alignItems: "center",
  },
  buttonText: { color: "#fff", fontWeight: "bold" },
});
```

---

> Tips Ujian: Kalau ragu syntax, ingat pola: `import → definisi komponen → StyleSheet.create()`. Hampir semua komponen RN mengikuti pola ini!

> Dokumentasi resmi: https://reactnative.dev/docs/components-and-apis
