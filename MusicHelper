package music

import java.io.InputStream
import java.util.Objects
import javazoom.jl.decoder.JavaLayerException
import javazoom.jl.player.Player

class MusicHelper {
    val isRunning: Boolean
        get() = thread != null
    val isCompleted: Boolean
        get() = !thread.isAlive()

    fun start() {
        Objects.requireNonNull(player)
        thread = Thread {
            try {
                player.play()
            } catch (e: JavaLayerException) {
                e.printStackTrace()
            }
        }
        thread.start()
    }

    fun stop() {
        if (isRunning) {
            thread.interrupt()
            thread = null
            if (player != null) {
                player.close()
            }
        }
    }

    fun setStream(inputStream: InputStream?) {
        try {
            player = Player(inputStream)
        } catch (e: JavaLayerException) {
            e.printStackTrace()
        }
    }

    companion object {
        private var player: Player? = null
        private var thread: Thread? = null
        fun getThread(): Thread? {
            return thread
        }

        fun getPlayer(): Player? {
            return player
        }
    }
}
