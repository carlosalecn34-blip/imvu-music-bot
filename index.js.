const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

// Sistema de cola de música
let currentQueue = [];
let isPlaying = false;

app.use(express.json());

// Servidor HTTP para mantener activo el servidor en Render
app.get('/', (req, res) => {
  res.send('Bot de Música IMVU activo 24/7');
});

// Endpoint para procesar comandos enviados desde el chat
app.post('/command', (req, res) => {
  const { command, args, user } = req.body;

  if (command === '!play') {
    const song = args.join(' ');
    if (!song) return res.json({ response: 'Escribe el nombre o link de la canción.' });
    
    currentQueue.push(song);
    return res.json({ response: `Añadido a la cola: ${song}` });
  }

  if (command === '!queue') {
    if (currentQueue.length === 0) return res.json({ response: 'La cola está vacía.' });
    return res.json({ response: `Canciones en cola: ${currentQueue.join(', ')}` });
  }

  if (command === '!skip') {
    if (currentQueue.length === 0) return res.json({ response: 'No hay nada que saltar.' });
    const skipped = currentQueue.shift();
    return res.json({ response: `Saltada: ${skipped}` });
  }

  return res.json({ response: 'Comando no reconocido.' });
});

app.listen(PORT, () => {
  console.log(`Servidor del bot ejecutándose en el puerto ${PORT}`);
});
