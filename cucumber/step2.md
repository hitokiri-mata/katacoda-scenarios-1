Realiza los siguientes pasos:

1) Agrega el siguiente escenario al final del archivo feature.

<pre class="file" data-filename="./features/alarma.feature" data-target="append">
  Scenario: Alarma no suena si esta apagada
    Given una alarma definida a las 7:05 AM
    And se encuentra apagada
    When son las 7:05:00 AM
    Then no esta sonando
</pre>

2) Ejecuta las pruebas `make cucumber`{{execute}}.

3) Lee los resultados, observa que indica que el step `Then no esta sonando` no está implementado.

4) Abre el archivo `./features/step_definitions/steps.rb` para implementar el step faltante.

5) Agrega el siguiente contenido al final del archivo de steps.

<pre class="file" data-filename="./features/step_definitions/steps.rb" data-target="append">
Given(/^se encuentra apagada$/) do
  @reloj.apagar!
end
</pre>

6) Ejecuta las pruebas `make cucumber`{{execute}}.