import { StatusBar } from 'expo-status-bar';
import React, { useState } from 'react';
import { View, Button, Text } from 'react-native';
import { Ionicons } from '@expo/vector-icons'; // Import Ionicons from @expo/vector-icons

export default function App() {
  const [isFlashlightVisible, setIsFlashlightVisible] = useState(false);
  const [isFlashlightOn, setIsFlashlightOn] = useState(false);
  const [counterValue, setCounterValue] = useState(0);
  const [isCounterVisible, setIsCounterVisible] = useState(false);

  const handleFlashlightButtonClick = () => {
    setIsFlashlightVisible(!isFlashlightVisible);
    setIsCounterVisible(false);
    setIsFlashlightOn(!isFlashlightOn);
  };

  const handleCounterButtonClick = () => {
    setIsCounterVisible(true);
    setIsFlashlightVisible(false);
  };

  const handleMinusOneButtonClick = () => {
    setCounterValue(counterValue - 1);
  };

  const handlePlusOneButtonClick = () => {
    setCounterValue(counterValue + 1);
  };

  const handleBackButtonClick = () => {
    setIsFlashlightVisible(false);
    setIsCounterVisible(false);
  };

  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      {isFlashlightVisible ? (
        <>
          <Ionicons
            name={isFlashlightOn ? 'flash' : 'flash-off'}
            size={100}
            color={isFlashlightOn ? 'yellow' : 'gray'}
            style={{ marginBottom: 20 }}
          />
          <Button
            title={isFlashlightOn ? 'Off' : 'On'}
            onPress={() => {
              setIsFlashlightOn(!isFlashlightOn);
            }}
          />
          <Button title="Back" onPress={handleBackButtonClick} />
        </>
      ) : (
        <>
          <Button title="Flashlight" onPress={handleFlashlightButtonClick} />
          {isCounterVisible && (
            <>
              <Text style={{ fontSize: 50 }}>{counterValue}</Text>
              <View style={{ flexDirection: 'row', marginTop: 10 }}>
                <Button title="-1" onPress={handleMinusOneButtonClick} />
                <Button title="+1" onPress={handlePlusOneButtonClick} />
              </View>
              <Button title="Back" onPress={handleBackButtonClick} />
            </>
          )}
          {!isCounterVisible && (
            <Button title="Counter" onPress={handleCounterButtonClick} />
          )}
        </>
      )}
      <StatusBar style="auto" />
    </View>
  );
}
