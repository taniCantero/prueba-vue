<template>
    <div class ="container">
        <h1>Lista de Tareas</h1>
        <!-- Esta seccion es una combinación de las dos vistas anteriores -->
        <div class="input-group">
            <input 
                v-model="newTask" 
                @keyup.enter="addTask" 
                placeholder="Añadir nueva tarea" 
                class="task-input" 
            />
            <button @click="addTask" class="add-button">Añadir</button>
        </div>
    
        <div v-if="tasks.length > 0" class="task-list">
            <div v-for="task in tasks" :key="task.id" class="task-item">
                <div class="task-info">
                    <h3 :class="{ completed: task.completed }">{{ task.todo }}</h3>
                    <span class="task-status" :class="{ 'pending': !task.completed, 'completed': task.completed }">
                        {{ task.completed ? 'Completada' : 'Pendiente' }}
                    </span>
                </div>
                <div class="task-actions">
                    <button class="complete-btn" @click="toggleTaskCompletion(task)">
                        {{ task.completed ? 'Desmarcar' : 'Completar' }}
                    </button>
                    <button class="delete-btn" @click="deleteTask(task)">Eliminar</button>
                </div>
            </div>
        </div>
    </div>
    
</template>

<script>
   // Esta sección debe permitir agregar tareas nuevas a la vez que extraer las tareas anteriores de la API
   export default {
    name: "TaskList",
    data() {
        return {
            newTask: "", // Campo de entrada para la nueva tarea
            tasks: [],   // Lista de tareas locales
        };
    },
    mounted() {
        this.fetchTasks(); // Cargar tareas automáticamente al montar el componente
    },
    methods: {
        // Cargar tareas desde la API
        async fetchTasks() {
            try {
                const response = await fetch("https://dummyjson.com/todos");
                const data = await response.json();
                this.tasks = data.todos;
            } catch (error) {
                console.error("Error al cargar las tareas:", error);
            }
        },
        
        // Añadir nueva tarea
        addTask() {
            if (this.newTask.trim() === "") return;

            const newTask = {
                todo: this.newTask,
                completed: false,
                id: Date.now(), 
            };

            // Añadir la nueva tarea al inicio de la lista
            this.tasks.unshift(newTask);
            this.newTask = ""; // Limpiar el campo de entrada después de agregar
        },

        // Eliminar una tarea específica de la lista
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },

        // Cambiar el estado de la tarea entre completada y no completada
        toggleTaskCompletion(task) {
            task.completed = !task.completed; // Cambiar el estado directamente
        },
    },
};
</script>

<style scoped>

.container {
    max-width: 600px;
    margin: 0 auto;
    text-align: center;
}

h1 {
    font-size: 40px;
    color: rgb(0, 0, 0);
   
}

button {
    padding: 10px 20px;
    margin: 5px;
    cursor: pointer;
    border: none;
    border-radius: 5px;
    font-size: 1em;
}

.load-btn {
    background-color: #61c7c2;
    color: rgb(0, 0, 0);
}

.task-list {
    margin-top: 20px;
}

.task-item {
    background-color: #f9f9f9;
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.task-info {
    flex-grow: 1;
}

.task-actions {
    display: flex;
    gap: 10px;
}

h3 {
    color: #000000; /* Color neutro para el texto de la tarea */
}

h3.completed {
    text-decoration: line-through; 
}

.task-status {
    display: inline-block;
    padding: 5px 10px;
    border-radius: 5px;
    font-weight: bold;
    margin-left: 10px;
}

.pending {
    background-color: rgb(250, 182, 55); /* Color naranja para 'Pendiente' */
    color: white;
}

.completed {
    background-color: rgb(215, 108, 224); 
    color: white;
}

.complete-btn {
    background-color: #83b8d1; 
    color: rgb(15, 15, 15);
    padding: 10px 15px;
    border-radius: 5px;
    border: none;
    cursor: pointer;
}

.complete-btn:hover {
    background-color: #c9ebf3; 
}

.delete-btn {
    background-color: #ff0f27; 
    color: rgb(0, 0, 0);
    padding: 10px 15px;
    border-radius: 5px;
    border: none;
    cursor: pointer;
}

.delete-btn:hover {
    background-color: #e65261; /* Rojo más oscuro al pasar el ratón */
}
</style>