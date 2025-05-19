interface SensorTemperatura {
    double lerTemperatura();
}

class SensorTemperaturaAntigo {
    public double getTempFahrenheit() {
        return 212.0;
    }
}

class AdaptadorSensorTemperatura implements SensorTemperatura {
    private SensorTemperaturaAntigo sensorAntigo;

    public AdaptadorSensorTemperatura(SensorTemperaturaAntigo sensorAntigo) {
        this.sensorAntigo = sensorAntigo;
    }

    public double lerTemperatura() {
        return (sensorAntigo.getTempFahrenheit() - 32) * 5 / 9; // conversão para Celsius
    }
}

class HondaPainel {
    public void exibirTemperatura(SensorTemperatura sensor) {
        System.out.println("Temperatura: " + sensor.lerTemperatura() + " °C");
    }
}

public class ClienteAdapter {
    public static void main(String[] args) {
        SensorTemperaturaAntigo sensorAntigo = new SensorTemperaturaAntigo();
        SensorTemperatura sensorAdaptado = new AdaptadorSensorTemperatura(sensorAntigo);

        HondaPainel painel = new HondaPainel();
        painel.exibirTemperatura(sensorAdaptado);
    }
}
