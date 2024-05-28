# ComponentesAngular

para filtro fechas con intervalos de meses: 

updateEndDate(){
    const fechaInicioValor= this.filtroForm.get('n_fechaInicio').value;
    if (fechaInicioValor) {
      const fechaInicio = new Date(fechaInicioValor)
      const fechaFin = new Date(fechaInicio.getTime());
      fechaFin.setMonth(fechaInicio.getMonth()+1);

      const fechaActual = new Date();
      fechaActual.setHours(0,0,0,0);

      const fechaFinal = fechaFin>fechaActual?fechaActual:fechaFin
      this.filtroForm.patchValue({ n_fechaFin: fechaFinal.toISOString().split('T')[0] });
      this.cdRef.detectChanges();
    }
    console.log(this.filtroForm.value.n_fechaInicio)
    console.log(this.filtroForm.value.n_fechaFin)
  }

  updateIniDate(){
    const fechaFinValor = this.filtroForm.get('n_fechaFin').value;
    if (fechaFinValor) {
      const fechaFin =new Date(fechaFinValor)
      const fechaIni = new Date(fechaFin.getTime());
      fechaIni.setMonth(fechaFin.getMonth()-1);

      console.log(fechaIni.toISOString().split('T')[0])

      this.filtroForm.patchValue({ n_fechaInicio: fechaIni.toISOString().split('T')[0] });
      this.cdRef.detectChanges();
    }
    console.log(this.filtroForm.value.n_fechaInicio)
    console.log(this.filtroForm.value.n_fechaFin)
  }


  codigo HTML

  <div class="col-2 col-sm-2 form-group">
      <label for="n_fechaInicio">Fecha de inicio</label>
      <input type="date" class="form-control" id="n_fechaInicio" (change)="updateEndDate()" [max]="maxDate"
          formControlName="n_fechaInicio">
          <br>
      </div>
      <div class="col-2 col-sm-2 form-group">
        <label for="n_fechaFin">Fecha de fin</label>
        <input type="date" class="form-control" id="n_fechaFin" (change)="updateIniDate()"  [max]="maxDate"
        formControlName="n_fechaFin">
        <br>
     </div>
