import React, { useState } from 'react';
import { StyleSheet, Text, View, Button } from 'react-native';

function FlashLight({ isOn, toggleLight, goBack }) {
  return (
    <View style={styles.container}>
      <Text style={styles.header}></Text>
      <View style={styles.flashlight}>
        <View
          style={[
            styles.light,
            {
              backgroundColor: isOn ? 'yellow' : 'black',
            },
          ]}
        />
        <View
          style={[
            styles.lightHandle,
            {
              backgroundColor: isOn ? 'gray' : 'black',
            },
          ]}
        />
      </View>
      <Button title={isOn ? 'Off' : 'On'} onPress={toggleLight} />
      <Button title="Back" onPress={goBack} />
    </View>
  );
}

function Counter({ count, increment, decrement, goBack }) {
  return (
    <View style={styles.container}>
      <Text style={[styles.header, styles.countText]}>{count}</Text>
      <Button title="+1" onPress={increment} />
      <Button title="-1" onPress={decrement} />
      <Button title="Back" onPress={goBack} />
    </View>
  );
}

export default function App() {
  const [showFlashLight, setShowFlashLight] = useState(false);
  const [showCounter, setShowCounter] = useState(false);
  const [count, setCount] = useState(0);
  const [isLightOn, setIsLightOn] = useState(false);

  const toggleFlashLight = () => {
    setShowFlashLight(true);
    setShowCounter(false);
  };

  const toggleCounter = () => {
    setShowCounter(true);
    setShowFlashLight(false);
  };

  const goBack = () => {
    setShowFlashLight(false);
    setShowCounter(false);
  };

  const increment = () => {
    setCount((prevCount) => prevCount + 1);
  };

  const decrement = () => {
    setCount((prevCount) => prevCount - 1);
  };

  const toggleLight = () => {
    setIsLightOn((prevIsOn) => !prevIsOn);
  };

  return (
    <View style={styles.container}>
      {showFlashLight && (
        <FlashLight isOn={isLightOn} toggleLight={toggleLight} goBack={goBack} />
      )}
      {showCounter && (
        <Counter count={count} increment={increment} decrement={decrement} goBack={goBack} />
      )}

      <View style={styles.topButtonContainer}>
        <Button title="FlashLight" onPress={toggleFlashLight} disabled={showFlashLight || showCounter} />
        <Button title="Counter" onPress={toggleCounter} disabled={showFlashLight || showCounter} />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  topButtonContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    paddingHorizontal: 20,
    width: '100%',
    marginTop: 20,
  },
  header: {
    fontSize: 24,
    marginBottom: 20,
  },
  flashlight: {
    width: 200,
    height: 400,
    borderRadius: 10,
    justifyContent: 'flex-start',
    alignItems: 'center',
    marginBottom: 20,
  },
  light: {
    width: 100,
    height: 200,
    borderRadius: 10,
    marginTop: 20,
  },
  lightHandle: {
    width: 20,
    height: 80,
    borderRadius: 20,
    backgroundColor: 'gray',
    marginTop: 10,
  },
  countText: {
    fontWeight: 'bold',
    fontSize: 32,
  },
});

