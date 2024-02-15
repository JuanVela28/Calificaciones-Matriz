# Calificaciones-Matriz
Juan Carlos Vela Mena. 3SB.

class CalificacionesM:
    def __init__(self, num_alumnos, num_asig):
        self.num_alumnos = num_alumnos
        self.num_asig = num_asig
        self.calificaciones = {}
        self.nombres_asig = []

    def ingresar_califs(self):
        self.nombres_asig = [input(f"Ingrese el nombre de la materia {i + 1}: ") for i in range(self.num_asig)]

        for i in range(self.num_alumnos):
            print(f"\nIngresar calificaciones para el Alumno {i + 1}:")
            calificaciones_alumno = {self.nombres_asig[j]: float(input(f"Ingrese la calificación para {self.nombres_asig[j]}: ")) for j in range(self.num_asig)}
            self.calificaciones[f'Alumno {i + 1}'] = calificaciones_alumno

    def show_califs(self):
        print("\nCalificaciones:")
        print("\t" + "\t".join(f"{materia}" for materia in self.nombres_asig))
        for alumno, calificaciones_alumno in self.calificaciones.items():
            print(f"{alumno}:", end="\t")
            for materia in self.nombres_asig:
                print(f"{calificaciones_alumno.get(materia, '')}\t", end="")
            print()

    def buscar_calificacion(self, alumno, materia):
        alumno_key = f'Alumno {alumno}'
        if alumno_key in self.calificaciones and materia in self.calificaciones[alumno_key]:
            return self.calificaciones[alumno_key][materia]
        else:
            return None

calificaciones_clase = CalificacionesM(num_alumnos=100, num_asig=6)

calificaciones_clase.ingresar_califs()

calificaciones_clase.show_califs()

alumno_buscar = int(input("\nIngrese el número de alumno a buscar (1-100): "))
asig_buscar = input("Ingrese el nombre de la materia a buscar: ")

calificacion_buscada = calificaciones_clase.buscar_calificacion(alumno_buscar, asig_buscar)

if calificacion_buscada is not None:
    print(f"\nLa calificación del Alumno {alumno_buscar} en la Materia {asig_buscar} es: {calificacion_buscada}")
else:
    print(f"\nEl Alumno {alumno_buscar} o la Materia {asig_buscar} no existen en la matriz.")


# Como yo lo veo, el programa corre mas rapido cuando las materias/asignaturas se colocan en las columnas de la matriz (en la parte superior) y los alumnos en las filas de la matriz (en la parte de la izquierda), porque carga mas rapido la lista de ariba a abajo que de izquierda a derecha, que en ese caso seria cuando se intercambian las posiciones de los alumnos y las materias/asignaturas
