# Generar Stat_button en condiciones
```xml
<!-- Recubrimiento exterior -->
<div class="oe_button_box" name="button_box">
    <!-- Boton con icono -->
    <button position="after" type="action" name="%(inventory_reader_exportation_action)d"
            class="oe_stat_button" icon="fa-file">
        
        <div class="o_field_widget o_stat_info">
            <span class="o_stat_value">
                <field string="Exportaciones" name="exportations_count" widget="statinfo"/>
            </span>
            <span class="o_stat_text">Exportaciones</span>
        </div>
    </button>
</div>
```