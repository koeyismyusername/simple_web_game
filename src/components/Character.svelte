<script>
  import { getDatabase, onValue, ref, set } from "firebase/database";

  const db = getDatabase();
  const dbRef = ref(db, "position/");
  const step = 50;

  let top;
  let left;

  document.addEventListener("keyup", handleKeyup);

  function handleKeyup(event) {
    switch (event.key.toUpperCase()) {
      case "ARROWUP":
        top -= step;
        break;
      case "ARROWDOWN":
        top += step;
        break;
      case "ARROWLEFT":
        left -= step;
        break;
      case "ARROWRIGHT":
        left += step;
        break;
      default:
        break;
    }

    set(dbRef, {
      top: top,
      left: left,
    });
  }

  onValue(dbRef, (snapshot) => {
    top = snapshot.val().top;
    left = snapshot.val().left;

    const character = document.querySelector("#character");
    character.style.left = `${left}px`;
    character.style.top = `${top}px`;
  });
</script>

<img
  src="https://avatar.maplestory.nexon.com/Character/JOLAEBGKCPHBBBOGNCMPJOEPMNOAKPKLLLLKFLOGOKNMKAHIAADDHNJIALJHKFLPDDOHDBKNDNGGHKENHCJLEDILPNDKNGLAOFCOJJBBKKFOMGJKDJBFOAIENNEJGDLBPFKEENCOILGKEGPFAPBBEKJIPMDJMCGLFLIANMJDGPOGPGFIMMCEFAIMPEJMMOGGCOBOMGPDJMCMKMJKAHBALBPDKLBBHEBJHJKFBGMOOOEBODDBILLMPIIMPAJEIEPM.png"
  alt="캐릭터 이미지"
  id="character"
/>

<style>
  #character {
    position: absolute;
  }
</style>
