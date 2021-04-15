# Macowins


## Requerimientos

  * modelar prendas
  * modelar ventas
  * modelar gestorVentasDiarias


## Diagrama de clases

<p align="center"> 
<img src="DDS 2021 - Macowins.png">
</p>


## Pseudocodigo

~~~
enum TipoPrenda {
  SACO, PANTALON, CAMISA
}


enum EstadoPrenda {
  int calcularPrecio(int precioBase);
    
  int valorPromocion = 5; //un valor cualquiera en este caso
    
  NUEVA {
      @Override
      int calcularPrecio(int precioBase) { return precioBase; }
  }, 
  PROMOCION {
      @Override
      int calcularPrecio(int precioBase) { return precioBase - valorPromocion; } 
  },
  LIQUIDACION {
      @Override
      int calcularPrecio(int precioBase) { return precioBase * 0.5; }
  };
}



class Prenda{

  int precioBase;

  TipoPrenda tipo;

  EstadoPrenda estado;


  int precio(){
    return estado.calcularPrecio(precioBase);
  }
}



enum ModoDePago {

  int coeficienteTarjeta;

  int calcularPrecioTotal(List<Prenda> prendas, int cantidadCuotas);
    
    
  EFECTIVO {
      @Override
      int calcularPrecioTotal(List<Prenda> prendas, int cantidadCuotas) { return sumList(prendas.precio()); }
  }, 
  TARJETA {
      @Override
      int calcularPrecioTotal(List<Prenda> prendas, int cantidadCuotas) { return sumList(prendas.precio()) + cantidadCuotas * coeficienteTarjeta + sumList(prendas.precio() * 0.01); } 
  };
}




class Venta{

  list<Prenda> prendas;
  
  LocalDate fechaVenta;
      
  ModoDePago modoDePago;
  
  int cantidadCuotas = 1; //por defecto 1, asi no rompe si la venta fue en Efectivo en "modoDePago.calcularPrecioTotal(prendas, cantidadCuotas)"
  
  
  
  int cantidadPrendas(){
    prendas.tamanioLista();
  }
  
  int precioTotal(){
    return modoDePago.calcularPrecioTotal(prendas, cantidadCuotas);
  }
}


class GestorDeVentas{

  list<Venta> ventas; //suponiendo que son todas las ventas de Macowins
  
  int GananciaDelDia(LocalDate dia){
    list<Venta> ventasDelDia = filterList(ventas, ventas.fechaVenta == dia);
    
    return sumList(ventasDelDia.precioTotal());
  }
}
~~~


## Alternativas

* En ves de usar Enum, usar Clases

  Almenos para TipoPrenda no seria util ya que no hay comportamiento. En las demas opciones es preferible usar Enum porque asi se limitan los valores que puede tomar el atributo

* Cachear el precio de la prenda. tratarla como un atributo

  No es necesario porque el calculo es bastante simple. Habria que revisarlo si la forma de hacer el calculo cambia

* Usar bool para ModoDePago en ves de un Enum

  Lo estoy evitando para no usar condicionales que no hacen falta. Ademas permite agregar mas tipos de modo de pago.

