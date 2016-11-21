.. |gh-src| image:: /_static/logos/GitHub-Mark-32px.png
            :scale: 40
            :target: https://github.com/VLSI-EDA/PoC/blob/master/src/io/ddrio/ddrio_in.vhdl
            :alt: Source Code on GitHub
.. |gh-tb| image:: /_static/logos/GitHub-Mark-32px.png
            :scale: 40
            :target: https://github.com/VLSI-EDA/PoC/blob/master/tb/io/ddrio/ddrio_in_tb.vhdl
            :alt: Source Code on GitHub

.. sidebar:: GitHub Links

   * |gh-src| :pocsrc:`Sourcecode <io/ddrio/ddrio_in.vhdl>`
   * |gh-tb| :poctb:`Testbench <io/ddrio/ddrio_in_tb.vhdl>`

.. _IP:ddrio_in:

ddrio_in
########

Instantiates chip-specific :abbr:`DDR (Double Data Rate)` input registers.

Both data ``DataIn_high/low`` are synchronously outputted to the on-chip logic
with the rising edge of ``Clock``. ``DataIn_high`` is the value at the ``Pad``
sampled with the same rising edge. ``DataIn_low`` is the value sampled with
the falling edge directly before this rising edge. Thus sampling starts with
the falling edge of the clock as depicted in the following waveform.

.. wavedrom::

   { signal: [
       {name: 'clk',             wave: 'H.L.H.L.H.L.H.L.H'},
       {name: 'pad',             wave: 'x2.3.4.5.2.3.x...', data: ['0', '1', '2', '3', '4', '5'], node: '..a.b.c.d.e.f..'},
       ['DataIn',
         {name: 'DataIn_low',    wave: 'x...2...4...2...x', data: ['0',      '2',      '4'],      node: '.....k...m...o.'},
         {name: 'DataIn_high',   wave: 'x...3...5...3...x', data: ['1',      '3',      '5'],      node: '.....l...n...p.'},
       ],
     ],
     edge: ['a~k', 'b~l', 'c~m', 'd~n', 'e~o', 'f~p'],
     foot: {text: 'PoC.io.ddrio.in'}
   }

.. code-block:: none

                __      ____      ____      __
   Clock          |____|    |____|    |____|
   Pad          < 0 >< 1 >< 2 >< 3 >< 4 >< 5 >
   DataIn_low      ... >< 0      >< 2      ><
   DataIn_high     ... >< 1      >< 3      ><

   < i > is the value of the i-th data bit on the line.

After power-up, the output ports ``DataIn_high`` and ``DataIn_low`` both equal
INIT_VALUE.

``Pad`` must be connected to a PAD because FPGAs only have these registers in
IOBs.



.. rubric:: Entity Declaration:

.. literalinclude:: ../../../../src/io/ddrio/ddrio_in.vhdl
   :language: vhdl
   :tab-width: 2
   :linenos:
   :lines: 78-90

Source file: :pocsrc:`io/ddrio/ddrio_in.vhdl <io/ddrio/ddrio_in.vhdl>`

