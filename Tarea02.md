		Tarea #02: "git rebase" y sus aplicaciones en un "pull request"

----- "git rebase":

  Sirve para aplicar commits en la parte superir de otra base tip.
  Su sipnosis se representa de la siguiente manera:

        git rebase [-i | --interactive] [options] [--exec <cmd>] [--onto <newbase>]
	  	[<upstream> [<branch>]]
	git rebase [-i | --interactive] [options] [--exec <cmd>] [--onto <newbase>]         
			--root [<branch>]              					            git rebase --continue | --skip | --abort | --edit-todo

  Si no se especifica <branch>, "git rebase" llevará a cabo una automática con "git
  checkout <branch>" antes de hacer cualquier otra cosa. De lo contrario, permanece
  en la rama actual.
  
  Si <upstream> no se especifica, el upstream sera configurado en la rama. <name>.
  remote y rama. Se utilizarán <name>. de ser ultizidados las opciones de merge y de 
  "--fork-point" se aumiran a este caso. Si no esta actualmente en cualquier rama o 
  si la rama actual no tiene configurado el upstream, el rebase se interrumpirá.
  
  Todos los cambios realizados por commit en la rama actual, pero que no están en 
  <upstream> se guardan en un área temporal. Este es el mismo conjunto de 
  confirmaciones que se muestra por git log <upstream>..HEAD; o git log 
  'fork_point'..HEAD, si --fork-pointestá activa; o git log HEAD, si la --rootopción 
  se especifica.

  La rama actual se restablece a <upstream> o <NewBase> si la opción --onto fue 
  suministrado. Esto tiene el mismo efecto como "git reset --hard" <upstream>(o 
  <NewBase>). "ORIG_HEAD" se establece en el punto en la punta de la rama antes del 
  restablecimiento.


----- "git-request-pull"
  
  Genera un resumen de los cambios pendientes.
  Su sipnosis se representa de la siguiente manera:

  	git request-pull [-p] <start> <url> [<end>]

  Donde:
  	"-p"      Inlcuye el texto del parche de salida.
	"<star>"  Empezar un commit.Esto da nombre a un commit que esta en el historial
	           del upstream.
  	"<url>"   La URL del repositorio para ser retirado.
	"<end>"   Commit termina en la HEAD. Esto da nombre al commit en el tip del 
	           historial que están pidiendo ser tirado.
  
  En otras palabras, "git-request-pull" genera una solicitud pidiendo al proyecto de
  upstream para tirar de los cambios en su árbol. La solicitud, impresa en la salida
  estándar, comienza con la descripción rama, resume los cambios e indica desde donde 
  se puede tirar.
  Se espera que al proyecto upstream para tener el commit nombrado "<star>" y la salida 
  le pide que integre los cambios realizados desde ese commit, hasta el commit nombrado       por "<end>", al visitar el repositorio llamado por "<url>".


----- "git rebase" en un "pull request"

  Una aplicacion es pasar una Rebase a "pull request". Cuando muchas personas están 
  trabajando en un proyecto simultáneamente, una "pull request" se puede a echarse a 
  perder rápidamente. Una vieja "pull request" ya no está al corriente de la línea 
  principal de desarrollo, y es necesario actualizarla antes de combinarla con un 
  proyecto.
  Tenemos un caso especifico donde ponemos a una rama ligada a un commit "X" dentro
  de la rama master, esta rama ligada se llamada "my-branch" y se desea llevarlo al 
  día con la ultima version de master. Por lo tanto, "my-branch" debe contener los 
  siguientes commits partiendo desde "X". En este caso se podria hacer un "merge",
  pero eso hace que tenga un merge con commits raros, entonces esto ocasiona que la 
  revisión del "pull request" sea mucho más dificíl. En su lugar, se puede hacer un
  rebase para solucionarlo.
