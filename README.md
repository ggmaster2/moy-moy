# moy-moy
//
//  ViewController.swift
//  moy moy
//
//  Created by Zoë Onion on 4/15/19.
//  Copyright © 2019 jairdreams.com. All rights reserved.
//

import UIKit
//4
import AVFoundation

class ViewController: UIViewController {
    
    //5 -
    var songPlayer = AVAudioPlayer()
    
    //15 -
    var hasBeenpaused = false
    
    //6
    func prepareSongAndSession() {
        
        do {
            //7 - Insert the song from our Bundle into our AVAudioPlayer
            songPlayer = try AVAudioPlayer(contentsOf: URL.init(fileURLWithPath: Bundle.main.path (forResource: "Sucker For Pain", ofType: "m4a")!))
            //8 - Prepare the song to be played
            songPlayer.prepareToPlay()
        
            //9 - Create an audio session
            let audioSession = AVAudioSession.sharedInstance()
            do {
                //10 - Set our Session category to playback music
                try audioSession.setCategory(AVAudioSession.Category.playback,
                    mode: .default, options: [])
                //11 -
            } catch let sessionError {
                print(sessionError)
            }
        } catch let songPlayerError {
            print(songPlayerError)
        }
    }
    
    

override func viewDidLoad() {
        super.viewDidLoad()
        //13
        prepareSongAndSession()
    }
    
    @IBAction func Play(_ sender: Any) {
        //14
        songPlayer.play()
   }
    
    //15
    var hasBeenPaused = false 
    
   @IBAction func Pause(_ sender: Any) {
        //16
        if songPlayer.isPlaying {
            songPlayer.pause()
            hasBeenPaused = true
        } else {
            hasBeenPaused = false
        }
        
    }

    @IBAction func restart(_ sender: Any) {
        //17 -
        if songPlayer.isPlaying || hasBeenPaused {
            songPlayer.stop()
            songPlayer.currentTime = 0
            
            songPlayer.play()
        } else {
            songPlayer.play()
        }
    }
    
    
}
