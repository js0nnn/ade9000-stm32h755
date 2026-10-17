# Example: moved to its own repo

The full example application, a hand-built **power quality analyzer** with a hand-soldered SMD ADE9000 on zero PCB, a dual-core STM32H755 and a real-time Python GUI, now lives in its own repository:

<p align="center">
  <a href="https://github.com/js0nnn/diy-power-quality-analyzer">
    <img src="https://raw.githubusercontent.com/js0nnn/diy-power-quality-analyzer/main/docs/hardware-annotated.jpg" width="100%" alt="Annotated photo of the DIY power quality analyzer board"/>
  </a>
</p>

<p align="center">
  <b><a href="https://github.com/js0nnn/diy-power-quality-analyzer">→ js0nnn/diy-power-quality-analyzer</a></b>
</p>

It uses the driver from this repository (`../driver`) and adds:

- SPI DMA burst reads of the ADE9000 waveform buffer
- CRC16-checked UART streaming at 921600 baud
- A PyQt6 visualizer with RMS, power, PF, THD and harmonic analysis
- Hardware and software block diagrams, photos and build steps
