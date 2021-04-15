# Macowins


## Requerimientos

  * modelar prendas
  * modelar ventas
  * modelar gestorVentasDiarias



## pseudocodigo

~~~
enum TipoPrenda {
  SACO, PANTALON, CAMISA
}


enum EstadoPrenda {
  int coeficiente(int precioBase);
    
  int valorPromocion = 5; //un valor cualquiera en este caso
    
  NUEVA {
      @Override
      int coeficiente(int precioBase) { return precioBase; }
  }, 
  PROMOCION {
      @Override
      int coeficiente(int precioBase) { return precioBase - valorPromocion; } 
  },
  LIQUIDACION {
      @Override
      int coeficiente(int precioBase) { return precioBase * 0.5; }
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
// lo planteo como un enum porque pienso que es probable que se agreguen funcionalidades nuevas segun un tipo de tarjeta, igual estoy arriesgandome a estar sobrediseñando..




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

## Diagrama de clases




## Alternativas

* En ves de usar enum, usar clases para TipoPrenda o EstadoPrenda

  Almenos para TipoPrenda no seria util ya que no hay comportamiento. Y para EstadoPrenda 

* cachear el precio de la prenda. tratarla como un atributo

  No es necesario porque el calculo es bastante simple. Habria que revisarlo si la forma de hacer el calculo cambia

* usar bool para ModoDePago en ves de un enum

  Lo estoy evitando para no usar condicionales que no hacen falta. Ademas permite agregar mas tipos de modo de pago.

